---
layout: post
title: Watir-Classic 3.1.0 Released!
date: 2012-08-22 22:30
author: bpettichord
comments: true
tags: [Releases]
---
<a href="http://www.flickr.com/photos/stewartho/2855517943/" title="Water Bomber by Stewart Ho, on Flickr"><img src="http://farm4.staticflickr.com/3076/2855517943_3336e61690.jpg" width="500" height="349" alt="Water Bomber"></a>

Hello everyone!

I'm happy to announce that another version of Watir-Classic has just been released - 3.1.0.
<!--more-->

Changelog:
<ul>
<li>Add <code>Browser#name</code>, which returns <code>:ie</code>.</li>
<li>Add <code>Dl#to_hash</code>.</li>
<li>Add support for <a href="https://github.com/watir/watirspec/blob/master/alert_spec.rb">Alert API</a>.</li>
<li>Add support for <a href="https://github.com/watir/watirspec/blob/master/screenshot_spec.rb"><code>Browser#screenshot</code> API</a>.</li>
<li><code>Browser#execute_script</code> returns now correct Ruby objects instead of <code>String</code>.</li>
<li><code>Browser#new</code> accepts ignored parameter to make API more compatible with Watir-WebDriver.</li>
<li><code>Element#drag_and_drop</code> methods work also with elements not in the viewport.</li>
<li>Fix <code>TextField#set</code> slow text entry.</li>
<li>Remove all <code>show_*</code> methods. Use element collection methods with <code>#each</code> instead. For example <code>browser.links.each {|link| puts link.href}</code>.</li>
<li>Remove already deprecated <code>Watir::Waiter</code>. Use <code>Watir::Wait</code> instead.</li>
<li>Remove already deprecated <code>WinClicker</code>.</li>
<li>Remove <code>Browser#(javascript_)dialog</code>. Use <code>Browser#alert</code> API instead.</li>
<li>Remove <code>ScreenCapture</code> module. Use <code>Browser#screenshot</code> API instead.</li>
<li>Remove Watir console. Use regular IRB or debugger instead.</li>
<li>Remove <code>Watir.log</code> method, <code>WatirLogger</code> and <code>DefaultLogger</code> classes. Use standard Ruby Logger instead.</li>
<li>Remove <code>Watir.until_with_timeout</code>. Use <code>Watir::Wait.until</code> instead.</li>
</ul>

Please try it out by executing:
<code>gem install watir watir-classic</code>

As usual: 

<ul>
<li>see all the changes at <a href="https://github.com/watir/watir-classic/commits/master/">github.com/watir/watir-classic/commits/master</a></li>
<li>updated API documentation is at <a href="http://rubydoc.info/gems/watir-classic">rubydoc.info/gems/watir-classic</a></li>
</ul>

<p>
