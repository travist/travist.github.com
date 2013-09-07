---
layout: post
title: "An online RSA public and private key generator"
date: 2013-09-06 21:22
comments: true
categories:
---
I was recently in a meeting where a person needed to generate a private and
public key for RSA encryption, but they were using a PC (Windows).  This is something
that is easily done via a terminal using ```ssh-keygen``` on Mac and Linux, however on Windows...
this tool is not easily accessible to the non-technical person.

It then occurred to me (and a head slapped followed), that I have fairly recently
published a library for Javascript RSA encryption which includes private and
public key generation for RSA encryption.  Not only that, but this is all
available online.

So, if anyone needs an online RSA key generator, look no further than <a target="_blank" href="http://travistidwell.com/jsencrypt/demo/">http://travistidwell.com/jsencrypt/demo</a>.
<!-- more -->

This directly maps to the Open Source GitHub repository found at <a target="_blank" href="https://github.com/travist/jsencrypt">https://github.com/travist/jsencrypt</a>, so
anyone can modify this website to make it better.

And here is an iframe of the RSA key generation tool.

<iframe src="http://travistidwell.com/jsencrypt/demo/index.html" width="100%" height="1200px" frameborder="0"></iframe>
