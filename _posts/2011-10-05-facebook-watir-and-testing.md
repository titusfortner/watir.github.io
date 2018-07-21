---
layout: post
title: Facebook, Watir And Testing
date: 2011-10-05 20:18
author: Jarmo Pertman
author_url: http://www.itreallymatters.net
comments: true
tags: [Blogs]
---
<!--more-->

<strong>Originally posted at <a href="http://itreallymatters.net/post/10991877834/facebook-watir-and-testing">itreallymatters.net</a> by <a href="http://www.itreallymatters.net/">Jarmo Pertman</a>.</strong>

<hr />

<p>
I’ve known some time now that <a href="http://www.facebook.com" target="_blank">Facebook</a> has been using <a href="http://www.watir.com" target="_blank">Watir</a> as their integration testing tool. Hell, there’s even a Facebook logo on the main page of <a href="http://watir.com" target="_blank">watir.com</a>. But today was a special day because i had to read one article about <a href="http://www.facebook.com/notes/facebook-engineering/watir-to-webdriver-unit-test-frameworks/10150314152278920" target="_blank">Facebook moving away from Watir</a>. 
</p>

<h3>Confusions</h3>

<p>
Since i’m one of the few core developers of Watir then this article made me notice statements which are not true or are just misleading. It seems to me that the author of that post doesn’t know the insights of Watir and other tools he’s mentioning or just uses wrong terminology by accident.
</p>

<h3>Watir &amp; JavaScript</h3>

<p>
First statement which forced me to questioning myself was the following: <i>“Watir automates the browser with JavaScript…”</i>.
</p>

<p>
It took me some time before i understood that the author had <i>FireWatir</i> in his mind and not the <i>Watir</i> itself. FireWatir was used to automate Firefox browser and it truly used JavaScript as it’s engine to perform all the automations. Watir on the other hand controls <i>Internet Explorer</i> and uses it’s <a href="http://en.wikipedia.org/wiki/OLE_Automation" target="_blank">OLE interface</a> instead to control the browser. This means in effect that there’s almost no JavaScript used in Watir.
</p>

<h3>Watir&nbsp;!= Watir-WebDriver&nbsp;!= WebDriver</h3>

<p>
The next statement causing confusion is: <i>“The Watir we adopted in 2009 has since been improved, integrating a new protocol called WebDriver which allows you to automate the browser more accurately and with more power than could previously be done with straight JavaScript.”</i>
</p>

<p>
First - Watir has been improved indeed when compared to year 2009 :) This is a good thing and a true statement. Second - Watir doesn’t integrate with the new protocol called WebDriver - it does still use OLE. I’m not exactly sure what the author means by the end of his statement about more accuracy and power. And of course - third - as mentioned already, Watir itself doesn’t use JavaScript and didn’t even do that in the year of 2009.
</p>

<p>
I think that you can call the WebDriver as a protocol, but the most famous implementation of that protocol is for sure <a href="http://code.google.com/p/selenium/" target="_blank">Selenium-WebDriver aka Selenium 2</a>. <a href="https://github.com/jarib/watir-webdriver" target="_blank">Watir-WebDriver</a> is a library written on top of Selenium-WebDriver’s <a href="http://www.ruby-lang.org" target="_blank">Ruby</a> bindings. In other words it is an improved API over Selenium’s API. At least this is the way, we, Watir-loving people like to think. It does even have some API improvements which <i>vanilla</i> Watir doesn’t have yet. There is a project called <a href="https://github.com/jarib/watirspec" target="_blank">WatirSpec</a>, which is <i>the</i> specification for Watir’s API. Even Watir itself doesn’t conform to that yet. But the ultimate goal is to make Watir-WebDriver and Watir 100% compatible with each other.<a href="http://watir.com/2011/08/11/watir-2-0/" target="_blank"> Latest releases of Watir</a> have been moving towards that goal.
</p>

<h3>Abandoning Watir</h3>

<p>
And then i have to read the saddest statement of that article: <i>“Once I understood all these factors, my course of action seemed clear: Abandon Watir, create a WebDriver client in PHP, and reuse our mature PHP unit test system for our browser tests. The WebDriver protocol was straightforward enough that I had a fully featured client in PHP by the end of a weekend’s work.”</i>
</p>

<p>
On the one hand i’m happy that the engineers in the Facebook try to make things better - having the same technologies used between different projects is always a good thing. On the other hand i’m not sure i understand as to why they had to create a new PHP WebDriver bindings. Looking from the main page of Selenium 2 i can see that there’s already two seemingly active projects doing just that - <a href="http://code.google.com/p/php-webdriver-bindings/" target="_blank">php-webdriver-bindings</a> and <a href="https://github.com/chibimagic/WebDriver-PHP" target="_blank">WebDriver-PHP</a>. Maybe engineers at Facebook had good reasons why not to use something already existing. Maybe they just like to feel more challenged and want to invent few bicycles in a while. I don’t know.
</p>

<h3>Conclusion</h3>

<p>
After all it was an interesting read. Since i’ve used Watir about 4 years now then it’s nice to read that someone else had similar or completely different solutions to the same problems. I like the thing about Facebook that it tries to be more open to the world when it comes to the topics of the tools and processes used to make, maintain and release such a widely used product.
</p>

<p>
On the other hand, posts having false information in them tend to have a strong effect on people using the tools under fire. Especially if this kind of information is originating from a trustworthy source. From that post it seems that it is time to abandon Watir since it is too old and not developed anymore. That’s just plain wrong. Watir is still actively developed and one of the biggest reasons why not to abandon Watir at this moment is that it is still the best automation tool for Internet Explorer. Watir-WebDriver’s IE driver is just not mature enough. Sorry, WebDriver guys. I would be happy to run all my tests with Watir-WebDriver since that would give me an opportunity to test with different browsers, but as long as IE is not working properly, then i just can’t do that. Since IE is the brittlest and still most used browser, then testing with that browser just seems to be mandatory.
</p>

<p>
I have to agree that if the person is not tied with all or some of these projects on a daily basis then it is hard to understand the difference between Watir, Watir-WebDriver and WebDriver. Maybe the biggest problem is just that the topics aren’t documented enough?
</p>
