---
layout: post
title: "Using Phantom.js with Node.js"
date: 2013-07-05 14:40
comments: true
categories:
---
{% img left http://phantomjs.org/images/phantomjs-logo.png PhantomJS %} Recently, I have had much interest in building web automation and testing tools
using Node.js.  The challenge, however, is when using Node.js for building tests
and automation, your options are pretty slim when picking your headless browser.
While <a href="http://zombie.labnotes.org/">Zombie.js</a> is a decent browser, it
uses JSDOM for its layout engine, whereas most of the web is ran on (or based off of) <a href="https://www.webkit.org/">WebKit</a>.  This
creates problems when trying to formulate accurate tests as well as benefit from
the ongoing development into the WebKit engine.  What really peaked my interest
was the project called <a href="http://phantomjs.org">Phantom.js</a> which is
basically a headless WebKit browser that exposes a JavaScript API to interact with
the browser.
<!-- more -->

Here is the problem... Phantom.js is not compatible with Node.js.  However, there is
a project that does expose the Phantom.js browser within the Node.js environment.
This project is called <a href="https://github.com/alexscheelmeyer/node-phantom">Node Phantom</a>,
which does a great job at bringing PhantomJS to NodeJS.  But, there is still
another issue where the API to this library is not easy to use like Zombie.js.

That is why I built a library which leverages the Node-Phantom library, but brings
in the <a href="http://zombie.labnotes.org/API">Zombie.js API</a> for ease of use.
This library is called <a href="https://github.com/travist/zombie-phantom">Zombie Phantom</a>
and I hope you enjoy it.

Also, please read the <a href="https://github.com/travist/zombie-phantom">project description</a> to
get an idea of the differences between this library and the Zombie API before using.

Here is an <a href="https://github.com/travist/zombie-phantom/blob/master/example.js">example</a> of how to use this library.

{% codeblock lang:javascript %}
var Browser = require('zombie-phantom');

var browser = new Browser({
  site: 'http://localhost:8888',
  addJQuery: false  // This page already has jQuery installed so use it...
});

browser.visit('/user/login', function() {
  browser.fill('#edit-name', 'admin', function() {
    browser.fill('#edit-pass', '123password', function() {
      browser.pressButton('#edit-submit', function() {
        console.log('You are logged in!');
        browser.close();
      });
    });
  });
});
{% endcodeblock %}

Enjoy...
