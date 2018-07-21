---
layout: post
title: watir-webdriver 0.5.2
date: 2012-02-01 15:25
author: bpettichord
comments: true
tags: [Releases]
---
<a href="http://www.flickr.com/photos/johnkay/3305073331/" title="Shower Water Snake feeding :) by Images by John 'K', on Flickr"><img src="http://farm4.staticflickr.com/3546/3305073331_149a4d746f_m.jpg" width="240" height="240" alt="Shower Water Snake feeding :)"></a>

<a href="https://rubygems.org/gems/watir-webdriver">watir-webdriver 0.5.2</a> has been released.
<!--more-->

Please note that watir-webdriver 0.5.0 brings some backwards incompatible changes:

<ul>
<li><a href="https://github.comwatir/watir/issues/21"><code>Watir::Select#selected_options</code> no longer returns array of strings, but array of <code>Watir::Option</code> objects</a></li>
<li><a href="https://github.comwatir/watir/issues/36">Finding elements by <code>:class</code> now matches partial class attributes.</a></li>
</ul>

Additionally, watir-webdriver 0.5.1 removes the following deprecated methods:

<ul>
<li><code>element_by_xpath</code> replaced by <code>.element(:xpath, '...')</code></li>
<li><code>elements_by_xpath</code> replaced by <code>.elements(:xpath, '...')</code></li>
</ul>

And deprecates the following methods:

<ul>
<li><a href="https://github.comwatir/watir/issues/24"><code>Browser#clear_cookies</code> - replaced by <code>Browser#cookies</code> API</a></li>
</ul>

Install it with

<code>gem install watir-webdriver</code>

As usual: 

<ul>
<li>see build history at <a href="http://travis-ci.org/#!watir/watir/builds">travis-ci.org/#!watir/watir/builds</a> (wait for a few seconds until older builds appear)</li>
<li>see all the changes at <a href="https://github.comwatir/watir/commits/master/">github.comwatir/watir/commits/master/</a></li>
<li>updated API documentation is at <a href="http://rubydoc.info/gems/watir-webdriver">rubydoc.info/gems/watir-webdriver</a></li>
</ul>

<p>
