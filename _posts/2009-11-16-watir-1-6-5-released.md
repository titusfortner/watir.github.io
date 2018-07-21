---
layout: post
title: Watir 1.6.5 Released
date: 2009-11-16 09:16
author: bpettichord
comments: true
tags: [ Releases]
---
<!--more-->
<h3>Version 1.6.5</h3>
For the latest version of release notes, please see <a href="http://github.com/bret/watir/blob/master/watir/NEWCHANGES">http://github.com/bret/watir/blob/master/watir/NEWCHANGES</a>
<h4>New Features (Both IE and Firefox)</h4>
<ul>
	<li>Browser.attach is now available.</li>
	<li>Browser.options and Browser.set_options are now available.</li>
	<li>Add support for definition lists, this adds these methods:
<ul>
	<li>dd, dt, dl, dds, dts, dls. (Jarib)</li>
</ul>
</li>
	<li>Hidden#visible? should always return false. (Jarib)</li>
	<li>New method execute_script.</li>
	<li>Add ElementCollections#size as alias of length. (Jarib)</li>
	<li>Some camelCase =&gt; snake_case renames (with aliasing). (Jarib)
<ul>
	<li>Image#fileCreatedDate =&gt; file_created_date</li>
	<li>Image#fileSize =&gt; file_size</li>
	<li>Image#hasLoaded? =&gt; loaded?</li>
	<li>SelectList#getAllContents =&gt; options</li>
	<li>SelectList#getSelectedItems =&gt; selected_options</li>
	<li>SelectList#clearSelection =&gt; clear</li>
	<li>SelectList#includes? =&gt; include?</li>
	<li>TextField#dragContentsTo =&gt; drag_contents_to</li>
	<li>Radio/Checkbox#isSet? =&gt; set?</li>
</ul>
</li>
	<li>Patch for winclicker fix. h<a href="//jira.openqa.org/browse/WTR-279">ttp://jira.openqa.org/browse/WTR-279</a> (Derek Berner)</li>
	<li>Add support for using a Regexp as the third argument (value) when locating checkboxes/radio buttons. (Jarib)</li>
	<li>Add support for  element. (Jarib)</li>
	<li>Add support and tests for  element. (Jarib)</li>
	<li>SelectList#select now supports Numeric arguments. (Jarib)</li>
	<li>Additional inspect implementations for both IE and FF. (Jarib)</li>
	<li>Added ElementCollections#{first,last}. (Jarib)</li>
	<li>Fixes for running on Ruby 1.9. (Jarib)</li>
</ul>
<h4>Firefox Improvements</h4>
<ul>
	<li>SelectList#set is now defined for Firefox. Like with IE, it is an alias for SelectList#select. [271]</li>
	<li>Element collections are now enumerable. This allows methods such as @select@ and @map@ to be used with methods such as @divs@ and @links@.</li>
	<li>FireWatir.attach is now available, analogous to IE.attach.</li>
	<li>Some Javascript errors that were being ignored, now raise Ruby exceptions.</li>
	<li>Added event handler which resets the context of document</li>
	<li>Fix bug that occurred when new page was automatically loaded. (Angrez, 3ef8b6) when page gets loaded automatically (Angrez)</li>
	<li>Changed code to use document_var, body_var, window_var, browser_var instead of "document", "body", "window", "browser" variables. (Angrez)</li>
	<li>Changed code to replace every quote (") in xpath query with (\") so that it doesn't give error while executing the xpath query (Angrez)</li>
	<li>Fire onchange event for FireWatir file fields. Closes WTR-286. (Jarib)</li>
	<li>Fixes for running and closing Firefox on Mac OS X</li>
	<li>Added functionality to allow Watir::Browser.attach with no arguments to open a new firefox window rather than taking over the existing focused window (Rob Aldred)</li>
	<li>Also modified some setup functions to correctly handle closed browsers, browserless windows and others (Rob Aldred)</li>
	<li>Add test and implementation for Firefox#status h<a href="//jira.openqa.org/browse/WTR-250">ttp://jira.openqa.org/browse/WTR-250</a> (Jarib)</li>
	<li> Two problems fixed with .click (jubishop)</li>
	<li>When chaining together element calls the @container becomes an HTMLElement, but there's no container_var defined for HTMLElement</li>
	<li>When an &lt;a tag has no href then element_type was returning nil.</li>
	<li>Fix bug in Firefox#document. change creating error class by eval in jssh socket to creating class with ruby.</li>
</ul>
<h4>IE Improvements</h4>
<ul>
	<li>Allow attach timeout to be accessed as an option. Thus:
<ul>
	<li>IE.set_options :attach_timeout =&gt; 5.0</li>
	<li>This was previously available as class method.</li>
</ul>
</li>
	<li>Fix for Autoit auto-registration. (Bret)</li>
	<li><a>Fix for Autoit auto-registration. (Bret) </a></li>
	<li><a>Fix for IE6, 7 and 8 file downloads. (Željko Filipin &amp; Jarmo Pertman)</a></li>
	<li><a>Replaced REXML with Nokogiri for xml parsing. (Aidy Lewis)</a></li>
	<li><a>Option now supports :label attribute http://jira.openqa.org/browse/WTR-297</a></li>
	<li><a>Patch for IE.close causing WIN32OLE errors http://jira.openqa.org/browse/WTR-304 (Tony)</a></li>
	<li><a>Watir::IE.inspect issue fixed: http://jira.openqa.org/browse/WTR-180 (Jarib)</a></li>
	<li><a>Fix for Browser#execute_script on IE7. (Jarib)</a></li>
	<li><a>Removed ActiveSupport dependency. (Jari</a></li>
</ul>
<h4>Structure Improvements</h4>
<ul>
	<li><a>Lots of rework of the FireWatir code, including removing duplication and</a><a> dead code, renaming variables, and simplifying code. Also a few performance</a><a>improvements.</a></li>
	<li><a>Rename source file names for consistency.</a></li>
</ul>
<h4><a>Unit Tests</a></h4>
<ul>
	<li><a>Add tests demonstrating known bugs.</a></li>
	<li><a>Make the "window" tests run more reliably.</a></li>
	<li><a>Relocate unreliable tests.</a></li>
	<li><a>Tag tests that are known to fail on IE or Firefox.</a></li>
	<li><a>Fixed one test that was failing on non-English platforms. (Jarib)</a></li>
	<li><a>New Rake task (:test) runs all tests.</a></li>
	<li><a>Use ci_reporter to provide more detailed test results for watirbuild.com</a></li>
	<li><a>Use xls transform to format results.</a></li>
	<li><a>Add WatirSpec submodule + load it in Rakefile if available. (Jarib)</a></li>
</ul>
