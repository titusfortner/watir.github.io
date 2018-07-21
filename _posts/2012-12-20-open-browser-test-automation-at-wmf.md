---
layout: post
title: Open browser test automation at WMF
date: 2012-12-20 07:34
author: Chris McMahon
author_url: http://chrismcmahonsblog.blogspot.com
comments: true
tags: [Blogs]
---
<!--more-->

<a title="By Roger McLassus (Picture taken and uploaded by Roger McLassus.) [GFDL (http://www.gnu.org/copyleft/fdl.html) or CC-BY-SA-3.0 (http://creativecommons.org/licenses/by-sa/3.0/)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3A2006-02-13_Drop-impact.jpg"><img width="256" alt="2006-02-13 Drop-impact" src="//upload.wikimedia.org/wikipedia/commons/thumb/f/f8/2006-02-13_Drop-impact.jpg/256px-2006-02-13_Drop-impact.jpg" /></a> Random photo: Impact of a drop of water

<strong>Originally posted at <a href="http://chrismcmahonsblog.blogspot.com/2012/12/open-browser-test-automation-at-wmf.html">chrismcmahonsblog.blogspot.com</a> by Chris McMahon.</strong>

<hr />

<div>
<br>
Almost a year ago I started working as <a href="https://www.mediawiki.org/wiki/User:Cmcmahon" target="_blank">QA Lead</a> for the <a href="https://wikimediafoundation.org/wiki/Home" target="_blank">Wikimedia Foundation</a>.&nbsp; Among other things, I had a mandate to create an automated browser testing practice at WMF.<br>
<br>
From the start I wanted this project to be a world class, completely open, reference implementation of such a project, using the best and most modern tools and practices I could find.&nbsp; I wanted this to be a project that anyone could read, anyone could run, and to which anyone could contribute.&nbsp; I wanted this to be an industry standard implementation of a well-designed, well-implemented, working browser test automation project.<br>
<br>
Around 2006 my career had veered off into a test automation approach that, while valid and useful in certain circumstances, would be inappropriate for the WMF project.&nbsp; And in the years since 2006, the tools and practices that were immature at the time had grown into mature, stable, powerful projects of their own.&nbsp; <br>
<br>
I set out to educate myself about the details of the cutting edge of browser test automation in every language.&nbsp; I visited Austin TX twice and San Francisco several times in the past year to discuss approaches to the project in person with experts on the subject.&nbsp; <br>
<br>
WMF hired <a href="https://twitter.com/zeljkofilipin/" target="_blank">Željko Filipin</a> in October 2012 specifically for the browser test automation project, and just this week we opened the curtain and turned on the lights.&nbsp; The WMF browser test automation project is in Ruby, using<br>
<br>
* page_object gem<br>
* watir-webdriver<br>
* selenium-webdriver<br>
* Cucumber<br>
* RSpec<br>
* rake<br>
* Jenkins integration<br>
<br>
The <a href="http://www.gossamer-threads.com/lists/wiki/wikitech/319419" target="_blank">initial announcement is here</a>. <br>
A <a href="https://www.mediawiki.org/wiki/QA/running_and_writing_browser_tests" target="_blank">first pass at technical documentation is here</a>, including instructions to run the tests locally if you want to see them in action on your own machine. <br>
Some <a href="https://www.mediawiki.org/wiki/Browser_testing/community_automated_browser_testing" target="_blank">community concerns are here</a>. <br>
The main code base is <a href="https://gerrit.wikimedia.org/r/#/q/status:merged+project:qa/browsertests,n,z" target="_blank">managed in gerrit</a> but there is a more accessible <a href="https://github.com/wikimedia/qa-browsertests" target="_blank">read-only mirror on github</a>. <br>
Our Jenkins instance is running on the <a href="http://www.cloudbees.com/" target="_blank">Cloudbees</a> service&nbsp; using <a href="https://saucelabs.com/" target="_blank">Sauce Labs</a>&nbsp; hosts, and the current <a href="https://wmf.ci.cloudbees.com/" target="_blank">test results are visible here</a>. <br>
If you would like to follow the project or contribute to it yourself, we are starting a community group you can join.&nbsp; Feel free to <a href="https://www.mediawiki.org/wiki/Groups/Proposals/Browser_testing" target="_blank">add yourself to the page here</a>&nbsp; to follow the project or contribute to it. <br>
<br>
Many people helped me along the way to making this project what it is.&nbsp; Hopefully I haven't left out anyone, feel free to remind me if I did! <br>
<br>
<a href="https://twitter.com/@chzy" target="_blank">Jeff Morgan</a> for creating the <a href="https://github.com/cheezy/page-object" target="_blank">page-object gem</a> and for answering tons of my questions<br>
<a href="https://twitter.com/jarib" target="_blank">Jari Bakken</a>, especially for <a href="https://speakerdeck.com/jarib/automating-130-browser-platform-and-language-combinations-without-going-insane" target="_blank">this presentation about webdriver in Ruby</a>. <br>
<a href="https://twitter.com/bramhaghosh" target="_blank">Brahma Ghosh</a><br>
<a href="https://twitter.com/charley_baker" target="_blank">Charley Baker</a><br>
<a href="https://twitter.com/alisterscott" target="_blank">Alister Scott</a> and his <a href="http://watirmelon.com/" target="_blank">Watirmelon blog</a><br>
<a href="https://twitter.com/marlenac" target="_blank">Marlena Compton</a>&nbsp; and <a href="https://twitter.com/m8ttyb" target="_blank">Matt Brandt</a>&nbsp; for discussing their experience at <a href="https://quality.mozilla.org/" target="_blank">Mozilla WebQA</a> with me. <br>
<a href="https://twitter.com/bpettichord" target="_blank">Bret Pettichord</a> for hosting&nbsp; the <a href="http://watir.com/test-automation-bazaar/" target="_blank">Test Automation Bazaar</a> <br>
<a href="https://twitter.com/aJimHolmes" target="_blank">Jim Holmes</a> of Telerik for hosting the <a href="http://www.telerik.com/automated-testing-tools/blog/12-05-07/telerik-testing-summit-wrapup.aspx" target="_blank">Telerik Test Summit </a><br>
<br>
And especially Željko for actually building the actual project! (And for <a href="http://kickurass.org/" target="_blank">kicking my ass</a>&nbsp; along the way, I still have a lot to learn.)
<div style="clear:both;"></div>
</div>
