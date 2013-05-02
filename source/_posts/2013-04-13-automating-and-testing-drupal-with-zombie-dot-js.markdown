---
layout: post
title: "Automating and Testing Drupal with Zombie.js"
date: 2013-04-13 14:18
comments: true
categories: [drupal, node.js, javascript, presentations]
---
Today I gave a presentation over Automating and Testing Drupal with Zombie.js at the
[Drupal Dallas Days Conference](http://drupaldallas.org/). I had a blast putting this
presentation together and I think just as much fun giving it.  I also used the incredible
library [Reveal.js](http://lab.hakim.se/reveal-js/#/) for the first time which is an
amazing way to build a presentation.  I hope you enjoy it...
<!-- more -->

## Presentation Video
<iframe width="100%" height="450px" src="http://www.youtube.com/embed/gd3L9i7Yb8Y" frameborder="0" allowfullscreen></iframe>

## Presentation Slides
 - [http://travistidwell.com/drupal-zombie](http://travistidwell.com/drupal-zombie)
 - [http://github.com/travist/drupal-zombie](http://github.com/travist/drupal-zombie)
<iframe width="100%" height="500px" src="http://travistidwell.com/drupal-zombie" frameborder="0" allowfullscreen></iframe>

## Overview
### The Bite
It all begins with the bite... Let's say you need to automate something repetitive
that you always do within the Drupal UI. Or, maybe you would like to write automated
tests for Drupal, but do not want to mess with the nasty installation and runtime of
Selenium IDE. Enter Zombie.js... a lightweight, insanely fast, headless browser for
testing and automation within a single Node.js package. No browser required.
You have just been bitten.

### The Infection
Installation is simple. Because it is a Node.js package, installation is as simple
as installing node.js on your local computer (http://nodejs.org), and then run
{% highlight bash %}
npm install zombie
{% endhighlight %}
You have just been infected.

### Walking
You realize that writing simple tests and automation tools is simple. You select
elements on the page using tools you know such as jQuery Selectors (Sizzle). The
API is easy and intuitive. You are now walking.

### Hunting and Feeding
You now cannot get enough... You are automating every mundane taks that you do
within the UI. You now have a powerful command line application at your fingertips
and realize that you do not need to build custom Services endpoints or custom Drush
commands to do what you want. You hunger for more... welcome to the hunting phase.

### Believing
You are now a believer. Zombie.js is amazing and will make your life easier.

