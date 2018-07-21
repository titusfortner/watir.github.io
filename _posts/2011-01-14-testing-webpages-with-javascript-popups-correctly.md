---
layout: post
title: Testing webpages with JavaScript popups correctly
date: 2011-01-14 13:11
author: Jarmo Pertman
author_url: http://www.itreallymatters.net
comments: true
tags: [Blogs]
---
<strong>Originally posted at <a href="http://www.itreallymatters.net/post/1482786902/testing-webpages-with-javascript-popups-correctly">itreallymatters.net</a> by <a href="http://www.itreallymatters.net/">Jarmo Pertman</a>.</strong>
<!--more-->

<hr />

Usually when a JavaScript dialog pops up at some webpage then there is a highly possibility that it shouldn't be there in the first place. It adds just more inconvenience to any user when needing to perform an additional click to get rid of some pointless message. If possible then solve the problem by removing those pointless usability mishaps altogether!

If there indeed exists some actual need of having a dialog window - perhaps the user is confirmed about starting a nuclear war and there's no sufficient possibility to <i>undo</i> that action - then it's needed to deal with those popups during automated testing. If the testing tool doesn't support this types of obstacles then I'm recommending to ditch that tool and choosing something else. For <a href="http://www.watir.com">Watir</a> there are a <a href="http://wiki.openqa.org/pages/viewpage.action?pageId=43909227">number of possibilities</a> to handle these dialogs, one more complex than another.

But there exists a very easy and elegant way to handle the JavaScript dialogs also. For some reason this technique hasn't been recommended much before in Watir's community until <a href="http://watirmelon.com/2010/10/31/dismissing-pesky-javascript-dialogs-with-watir/">Alister Scott wrote about it in his blog</a>. The main idea is to override the JavaScript dialog functions.

I'm writing my own blog post on that topic because I don't agree with everything Alister has written. He's recommending to override the functions to <code>return true</code>, but i don't think that this is a correct way to do. Main reason for my thoughts is that it's just not simulating the real functions properly. In real scenario, <i>alert</i> returns <code>true</code> in Firefox and <code>undefined</code> in IE. It doesn't matter though since no-one is using return value of an alert for any functionality, right? At least i hope so. But it's different altogether for <i>prompt</i> and <i>confirm</i>! Check out the following output from JavaScript console:


    &gt;&gt;prompt(&quot;enter!&quot;)
    &quot;info&quot;
    &gt;&gt;prompt(&quot;cancel!&quot;)
    null
    &gt;&gt;confirm(&quot;yes!&quot;)
    true
    &gt;&gt;confirm(&quot;no!&quot;)
    false

<a href="https://gist.github.com/663313#file_console.js">gist.github.com/663313#file_console.js</a>

As you can see then if user enters anything into the <i>prompt's</i> text field then that value is returned from the function and if he decides to click on a <code>Cancel</code> instead then <code>null</code> is returned. For the <i>confirm</i>, <code>true</code> was returned when "<i>OK</i>" was clicked and <code>false</code> otherwise.

Since both of the <i>confirm</i> and <i>prompt</i> might return different values then these values might be used in web pages for different functionality. This means that they should be simulated to work in both ways also in tests. Instead of returning <code>true</code> all the time, a different values should be returned as needed:

    # don't return anything for alert
    browser.execute_script(&quot;window.alert = function() {}&quot;)

    # return some string for prompt to simulate user entering it
    browser.execute_script(&quot;window.prompt = function() {return 'my name'}&quot;)

    # return null for prompt to simulate clicking Cancel
    browser.execute_script(&quot;window.prompt = function() {return null}&quot;)

    # return true for confirm to simulate clicking OK
    browser.execute_script(&quot;window.confirm = function() {return true}&quot;)

    # return false for confirm to simulate clicking Cancel
    browser.execute_script(&quot;window.confirm = function() {return false}&quot;)

<a href="https://gist.github.com/663313#file_dialogs.rb">gist.github.com/663313#file_dialogs.rb</a>

This code works with Watir, but not for FireWatir for some reason. I'm suspecting that FireWatir's JavaScript execution doesn't happen in the same scope as the page under test. This same technique might work with any testing tool that allows to execute JavaScript on the page. You'd just have to perform <code>execute_script</code> right before interacting with an element which triggers the dialog.

Since <a href="http://rubygems.org/gems/watir-webdriver">Watir-Webdriver</a> returns the executed JavaScript back to the Ruby then it allows for even <a href="https://github.com/jarib/watir-webdriver/blob/master/lib/watir-webdriver/extensions/alerts.rb">cooler solutions</a> where you can verify that an <i>alert</i> was shown indeed. For the <i>prompt</i> and <i>confirm</i>, the actual behavior of the web page itself should be enough for verification.

Hopefully next time if you happen to see any JavaScript dialog, you remember that it's possible to get rid of them very easily.
