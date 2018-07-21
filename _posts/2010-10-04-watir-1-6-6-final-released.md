---
layout: post
title: Watir 1.6.6 final released
date: 2010-10-04 14:04
author: bpettichord
comments: true
tags: [Releases]
---
Hello (fire)watirists!

We are happy to announce that a (very) long-waited (Fire)Watir 1.6.6 final gem is out!
<!--more-->
You can check out changelog at <a href="http://github.com/bret/watir/blob/master/CHANGES">http://github.com/bret/watir/blob/master/CHANGES</a>

Feel free to give it a test drive. Here are the basic instructions.

Make sure your local gem system is up to date.

<code>gem update --system</code>

run <code>gem -v</code> at the command line, you should be running 1.3.7

Windows:

<code>gem install watir</code>

Mac or Linux:

<code>sudo gem install firewatir</code>

...and give it a go. Try to use it with your existing test suites and so on to see if there are any issues.

If there are any problems then:
<ol>
	<li>Fix it and send a pull request on Github, our main github repo: <a href="http://github.com/bret/watir">http://github.com/bret/watir</a> This is the preferred way of accepting patches, we're happy to work with you on how to do this, github also has extensive docs on how to fork and submit a pull request.</li>
	<li>Add it to our JIRA tracker: <a href="http://jira.openqa.org/browse/WTR">http://jira.openqa.org/browse/WTR</a> If you need help with that let us know.</li>
</ol>
If you do have time and can help, please let us know, we can take any help from documentation to running tests on various OSes. We're a friendly project and would be happy to mentor you if you and/or your company is willing to put in the time.

Cheers,

<a href="http://watir.com/team/">The Watir Team</a>

Update: The following functionality is included.

<strong>Version 1.6.6
</strong>

<strong>IE improvements</strong>
<ul>
	<li>#elements_by_xpath uses now Nokogiri's xpath method instead of search (Matt Baker)</li>
	<li>Element#style returns now currentStyle. Closes http://jira.openqa.org/browse/WTR-444 (Jarmo Pertman)</li>
	<li>Element#visible? doesn't return false anymore for disabled elements (Charley Baker)</li>
	<li>TH elements texts are included into Table#to_a results. Closes http://jira.openqa.org/browse/WTR-445 (Jarmo Pertman)</li>
	<li>Added TableRow#to_a method which returns an array of the texts of the cells for the table row. Closes http://jira.openqa.org/browse/WTR-445 (Jarmo Pertman)</li>
	<li>Added an optional numeric parameter max_depth for Table#to_a and TableRow#to_a for getting text values for nested tables. Closes http://jira.openqa.org/browse/WTR-445 (Jarmo Pertman)</li>
	<li>#close will close the browser even if #wait raises an Exception. Closes http://jira.openqa.org/browse/WTR-443 (Jarmo Pertman)</li>
	<li>Added #element and #elements methods for locating non-specific elements. Closes http://jira.openqa.org/browse/WTR-103 (Hugh McGowan)</li>
	<li>#click_no_wait fixes and improvements. Closes http://jira.openqa.org/browse/WTR-320 and http://jira.openqa.org/browse/WTR-449 (Jarmo Pertman)</li>
	<li>#wait will raise a Timeout::Error if page hasn't been loaded within 5 minutes. Closes http://jira.openqa.org/browse/WTR-452 (Bret)</li>
	<li>Fixed a problem when #wait blocked forever. Closes http://jira.openqa.org/browse/WTR-446 (Jarmo Pertman)</li>
</ul>
<strong>Firefox improvements</strong>
<ul>
	<li> Added close_all method to firefox. Closes http://jira.openqa.org/browse/WTR-222 (Angrez)</li>
	<li>Fixed status method for firefox. (Angrez)</li>
	<li>Fixed url method for firefox. Closes http://jira.openqa.org/browse/WTR-428 (Alister Scott)</li>
	<li>Added JRuby support (Ian Dees)</li>
	<li>Forcing to use ActiveSupport 2.3.9 due to incompatibilities with newer versions (Jarmo Pertman)</li>
</ul>
<strong>Cleanup &amp; Maintenance</strong>
<ul>
	<li> Some rdoc cleanup (marekj)</li>
	<li>README changes (Željko Filipin)</li>
	<li>Removed Watir::Utils (Jarmo Pertman)</li>
	<li>It is now possible to execute unit-tests within gems with `rake test` (Jarmo Pertman)</li>
	<li>Don't output unnecessary information to stdout in FireWatir unit-tests (Željko Filipin)</li>
	<li>Update the 3 gem projects to each use the common readme file (Bret)</li>
</ul>
The whole Changelog is available at <a href="http://github.com/bret/watir/compare/v1.6.5...v1.6.6">http://github.com/bret/watir/compare/v1.6.5...v1.6.6</a>
