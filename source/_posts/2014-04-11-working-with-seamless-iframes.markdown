---
layout: post
title: "Working with Seamless iFrames"
date: 2014-04-11 22:31:14 -0500
comments: true
categories: 
---
As a web developer, one of the things that I have learned is that old conventions should NOT apply to modern practices.
iFrames is a great example of a wonderful web technology that is shunned today based on old impressions and existing bad practices. But, when it comes to iframes, you should not base your impressions off of the applications of that technology, but off of the technology itself.  And as it turns out, iFrames are amazing if used correctly.
<!-- more -->
So, what is it about iFrames that people have a sour opinion?  Well, for one thing, they can be abused, and unfortunately people LOVE to abuse iframes. My rule of thumb is this...
__Do not use an iframes to encapsulate an iterface that changes context__.  What I mean by this is you should not use an iframe if the page you are iframing has the capability of navigating a person away from a single purpose (like iframing all of https://youtube.com vs. just iframing a single video in YouTube).

Another problem with iframes is that they are kind of hard to work with... As it turns out, trying to create an iframe that appears to your visitor as a single seamless interface is not an easy thing to do. For this reason, I decided to create a single library that does all of the hard work for you. It is called [Seamless.js](http://travistidwell.com/seamless.js/index.html) and I hope you like it.

Click on these links to check out Seamless.js:

  http://www.travistidwell.com/seamless.js/index.html (Seamless.js Website)</li>
  https://github.com/travist/seamless.js (Github Project Page)