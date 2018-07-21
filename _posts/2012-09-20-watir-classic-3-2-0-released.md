---
layout: post
title: Watir-Classic 3.2.0 Released!
date: 2012-09-20 20:25
author: bpettichord
comments: true
tags: [Releases]
---
<a href="http://www.flickr.com/photos/laszlo-photo/4093575863/" title="When Water Drops Collide by laszlo-photo, on Flickr"><img src="http://farm3.staticflickr.com/2648/4093575863_9ba39f1a07.jpg" width="500" height="333" alt="When Water Drops Collide"></a>

Hello everyone!

I'm happy to announce that Watir-Classic 3.2.0 has been released!
<!--more-->

Changes:
<ul>
<li>Add <code>Element#browser</code> method as an alias for <code>Element#page_container</code>.</li>
<li>Fix <code>SelectList#{select|clear}</code> to fire <code>onChange</code> events for <code></code> element.</li>
<li><code>Watir::Browser</code> is now a <code>class</code> instead of a <code>module</code> - beware if you're monkey-patching.</li>
</ul>

As usual: 

<ul>
<li>Put it into your Gemfile: <code>gem "watir-classic"</code></li>
<li>Or install it manually with: <code>gem install watir-classic</code></li>
<li>see all the changes at <a href="https://github.com/watir/watir-classic/commits/master/">github.com/watir/watir-classic/commits/master</a></li>
<li>updated API documentation is at <a href="http://rubydoc.info/gems/watir-classic">rubydoc.info/gems/watir-classic</a></li>
</ul>

<p>
