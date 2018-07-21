---
layout: post
title: Debugging and Improving Watir’s click_no_wait Method
date: 2010-12-28 10:56
author: Jarmo Pertman
author_url: http://www.itreallymatters.net
comments: true
tags: [Blogs]
---
<!--more-->
<strong>Originally posted at <a href="http://www.itreallymatters.net/post/1366392123/debugging-and-improving-watirs-click-no-wait-method">itreallymatters.net</a> by <a href="http://www.itreallymatters.net/">Jarmo Pertman</a>.</strong>

<hr />

I’ve written about <a href="http://www.itreallymatters.net/post/378669758/debugging-watirs-click-no-wait-method-problems">debugging Watir’s click_no_wait method problems</a> before. This time i’m gonna do it again because starting from <a href="http://rubygems.org/gems/watir">Watir 1.6.6</a> the <code>#click_no_wait</code> method itself has changed along with the way to debug it’s problems.

In this post i’m gonna also write more about the inner-workings of <code>#click_no_wait</code> and the changes made to it in Watir 1.6.6.

There was mainly 3 motivations to change <code>#click_no_wait</code>:

<ul>
	<li>Make it faster!</li>
	<li>Make it easier to debug!</li>
	<li>Make the code itself cleaner and better!</li>
</ul>

<h3>Making it Faster</h3>

Before going into the dirty details how it became faster i’m gonna give a short overview how it was working before the changes. The main parts of the <code>#click_no_wait</code> were the following methods:

	# watir/element.rb
	def click_no_wait
	  assert_enabled

	  highlight(:set)
	  object = &quot;#{self.class}.new(self, :unique_number, #{self.unique_number})&quot;
	  @page_container.eval_in_spawned_process(object + &quot;.click!&quot;)
	  highlight(:clear)
	end

	# watir/page-container.rb
	def eval_in_spawned_process(command)
	  command.strip!
	  load_path_code = _code_that_copies_readonly_array($LOAD_PATH, '$LOAD_PATH')
	  ruby_code = &quot;require 'watir/ie'; &quot;
	  ruby_code &lt;&lt; &quot;pc = #{attach_command}; &quot; # pc = page container
	  ruby_code &lt;&lt; &quot;pc.instance_eval(#{command.inspect})&quot;
	  exec_string = &quot;start rubyw -e #{(load_path_code + '; ' + ruby_code).inspect}&quot;
	  system(exec_string)
	end

	# watir/ie.rb
	def _code_that_copies_readonly_array(array, name)
	  &quot;temp = Array.new(#{array.inspect}); #{name}.clear; temp.each {|element| #{name} &lt;&lt; element}&quot;
	end

<a href="https://gist.github.com/634798#file_click_no_wait.rb">gist.github.com/634798#file_click_no_wait.rb</a>

The main entrypoint is of course the <code>#click_no_wait</code> method itself which executes <code>#eval_in_spawned_process</code> in page-container. That in turn runs <code>start rubyw</code> with a <code>system</code> execution in a separate Ruby process where all the dirty work is done. The job consists of the following components:

<ul>
	<li>Loading Watir;</li>
	<li>Attaching to the browser window;</li>
	<li>Locating the element with an unique identifier and performing clicking on it.</li>
</ul>

The most time consuming part is not directly visible from the code above, but it was a require statement for <code>watir/ie</code>. This require statement triggered loading of everything in Watir. Even the things which are never needed in the “limited sandbox” of <code>#click_no_wait</code>. If you think of it then only core of Watir’s features are needed there to attach to the browser, locate the element and perform click on it. Every other advanced feature is not possible to use by <code>#click_no_wait</code>! Attaching to the browser, locating the element and performing click on it is pretty fast.

I inspected <code>watir/ie.rb</code> file and started to pick out all the require statements which might be needed in that sandbox. I ended up creating a separate file called <code>watir/core.rb</code> where only necessary files would be loaded. The file itself is loaded also by <code>watir/ie.rb</code> so everything would be available if using Watir normally. In other words, <code>core.rb</code> is a subset of files needed by Watir. This change itself made <code>#click_no_wait</code> to perform <a href="http://jira.openqa.org/browse/WTR-449">2-3 times faster</a> on my machine! That was enough for the time.

<h3>Making it Easier to Debug</h3>

As also written in the <a href="http://www.itreallymatters.net/post/378669758/debugging-watirs-click-no-wait-method-problems">previous post</a> then the fact that everything is done in a separate Ruby process is giving the feature of not blocking, but taking away the advantage of seeing any errors on the console window as you’d normally expect. This means that usually nothing is clicked and nothing is shown on the console in case of some problem. Using debugger would not help much either since the problem itself was happening on a spawned Ruby process with no visible output on the screen (yes, you could have set a breakpoint to <code>Element#click!</code>, but that wouldn’t have helped much if the error occurred before getting to that point). Also, for trying to change anything to happen differently in that spawned process with monkey-patching would have involved of overriding the whole contents of <code>#eval_in_spawned_process_method</code>. Not a nice way to solve problems, i’d say.

I wanted to achieve some possibility to debug these problems easily without any need of using debugger or monkey-patches. I wanted to use regular Ruby’s <code>$DEBUG</code> variable. To achieve that i extracted the command, which is given to the <code>system</code> method into separate method which would return a little bit different command depending of the value of <code>$DEBUG</code>:

	def click_no_wait
	  # ...
	  system(spawned_click_no_wait_command(ruby_code))
	end

	def spawned_click_no_wait_command(command)
	  command = &quot;-e #{command.inspect}&quot;
	  unless $DEBUG
	    &quot;start rubyw #{command}&quot;
	  else
	    puts &quot;#click_no_wait command:&quot;
	    command = &quot;ruby #{command}&quot;
	    puts command
	    command
	  end
	end

<a href="https://gist.github.com/634798#file_click_no_wait_debug.rb">gist.github.com/634798#file_click_no_wait_debug.rb</a>

If <code>$DEBUG</code> is set to <code>false</code> (which is the default case) then <code>#click_no_wait</code> works as usual, but if it’s set to <code>true</code> then it will output the executed command itself and will wait for the spawned Ruby process to exit so it’s possible to see all the error messages if any.

This approach also gives the opportunity to monkey-patch the executed command, which in turn allows to write some tests for the method itself.

To make it plain and clear then this is the way to turn on debugging for <code>#click_no_wait</code>:


	$DEBUG = true
	browser.button(:id =&gt; &quot;something&quot;).click_no_wait

<a href="https://gist.github.com/634798#file_click_no_wait_debug_on.rb">gist.github.com/634798#file_click_no_wait_debug_on.rb</a>

<h3>Making the Code Itself Cleaner and Better</h3>

The original code had some commented out code and over-generalisation. There were <code>instance_eval</code>’s and all other neat tricks which were not needed at all. The most cumbersome was the method called <code>_code_that_copies_readonly_array</code> defined in the global scope with a slightly funny comment - “why won’t this work when placed in the module (where it properly belongs)” - i even tried to move that method into the module where it actually worked. A valid case of comments getting out of sync? The change allowed to delete that method entirely and not use <code>instance_eval</code> and friends to make whole code more understandable. The resulting code is like this:

	def click_no_wait
	  assert_exists
	  assert_enabled
	  highlight(:set)
	  element = &quot;#{self.class}.new(#{@page_container.attach_command}, :unique_number, #{self.unique_number})&quot;
	  ruby_code = &quot;require 'rubygems';&quot; &lt;&lt;
	          &quot;require '#{File.expand_path(File.dirname(__FILE__))}/core';&quot; &lt;&lt;
	          &quot;#{element}.click!&quot;
	  system(spawned_click_no_wait_command(ruby_code))
	  highlight(:clear)
	end

<a href="https://gist.github.com/634798#file_click_no_wait_refactored.rb">gist.github.com/634798#file_click_no_wait_refactored.rb</a>

Of course in the end it is all just a matter of taste. There is only one small problem with this code - usage of Rubygems. It is in my pipeline to remove it’s usage without making code look much uglier (there’s no way i’m gonna add back that <code>_code_that_copies…</code> method!) and making <code>#click_no_wait</code> even faster.

Taking into the consideration the fact that these changes involved changing core code then i’m quite happy that they got released into the wild with only one (known) <a href="http://jira.openqa.org/browse/WTR-459">bug</a>!
