---
layout: post
title: "Authenticating Flatiron.js with Passport.js"
date: 2012-09-28 19:13
comments: true
categories:
---
So, I have fallen in love with [Flatiron.js](http://flatironjs.org).  For those who
are not familiar with this framework, it is basically an application framework for
Node.js.  Obviously, it isn't the only framework out there, but I would like to argue
that it is THE ONLY framework doing things right with JavaScript on the server side.
My reasons for this statement are backed by how it utilizes <strong>RVP</strong> instead
of <strong>MVC</strong> considering the isomorphic nature of Server-side to Client-side
libraries.  For more foundation to this statement, please read [Scaling Isomorphic Javascript Code](http://blog.nodejitsu.com/scaling-isomorphic-javascript-code);
it is a fantastic read.

Regardless, one of my major complaints with Flatiron.js was that it lacks in OAuth.
Looking around the Node.js community, there is a clear winner when it comes to OAuth, which
is [Passport.js](http://passportjs.org). But, there is a problem... Passport.js was
built on top of the [Express.js](http://expressjs.com) applicaton framework and not Flatiron.js.
Although, Express.js libraries are [Connect.js](http://www.senchalabs.org/connect) compatible,
and Flatiron.js is also Connect.js compatible, this isn't enough to provide a clean
integration between Passport.js and Flatiron.js.  So, to solve this issue, I created
a library that takes care of the integration work for you.  It is called [Flatiron Passport](https://github.com/travist/flatiron-passport),
and I would love for you to check it out...
<!-- more -->

Here is the readme from this library...

## Passport.js integration for FlatIron web framework.
This package allows [Flatiron.js](http://flatironjs.org) applications to easily use the
[Passport.js](http://passportjs.org) authentication framework.

There are only two things that are different between using this API and using the regular Passport API.

1.) Instead of calling...

{% codeblock lang:javascript %}
var express = require('express');
var passport = require('passport');
var app = express();
// ... BOILERPLATE SETUP CODE GOES HERE ...
app.use(passport.initialize());
app.use(passport.session());
{% endcodeblock %}

You simply need to call...

{% codeblock lang:javascript %}
var flatiron =      require('flatiron');
var fipassport =    require('flatiron-passport');
var app =           flatiron.app;
// ... BOILERPLATE SETUP CODE GOES HERE ...
app.use(fipassport);
{% endcodeblock %}

2.) Now anywhere you would use the variable passport, you replace that with fipassport in your app, like so...

{% codeblock lang:javascript %}
passport.use(new LocalStrategy(function(username, password, done) {
  ...
  ...
});

passport.serializeUser(function(user, done) {
  ...
  ...
});

passport.deserializeUser(function(id, done) {
  ...
  ...
});

passport.authenticate(.....)
{% endcodeblock %}

You simply call this instead...

{% codeblock lang:javascript %}
fipassport.use(new LocalStrategy(function(username, password, done) {
  ...
  ...
});

fipassport.serializeUser(function(user, done) {
  ...
  ...
});

fipassport.deserializeUser(function(id, done) {
  ...
  ...
});

fipassport.authenticate(.....)
{% endcodeblock %}

Please refer to the included example to get a better idea....

### Install

{% highlight bash %}
npm install flatiron-passport
{% endhighlight %}

## Example: From the example folder...

{% codeblock lang:javascript %}
var fs =            require('fs')
var flatiron =      require('flatiron');
var LocalStrategy = require('passport-local').Strategy
var fipassport =    require('flatiron-passport');
var app =           flatiron.app;

// You would not usually have these lines...
// This is just to store the username in memory.
var global_user = '';
var global_pass = '';

// Use the passport strategy.
fipassport.use(new LocalStrategy(function(username, password, done) {

  // You would not normally have these lines...
  // This is just to store it in memory for use later.
  global_user = username;
  global_pass = password;

  // Use this as you normally would in Passport.js.
  // But for now just
  // hard-code the user object.
  done(null, {
    id: 1234,
    username: username,
    password: password
  });
}));

// Serialize based on the user ID.
fipassport.serializeUser(function(user, done) {

  // @todo: Save your user to the database using the ID as a key.
  done(null, user.id);
});

// Load the user and return it to passport.
fipassport.deserializeUser(function(id, done) {

  // @todo:  Load your user here based off of the ID, and call done with
  // that user object.
  done(null, {
    id:id,
    username:global_user,
    password:global_pass
  });
});

// Use http and flatiron-passport.
app.use(flatiron.plugins.http);
app.use(fipassport);

// Get the front page.
app.router.get('/', function() {
  if (this.req.isAuthenticated()) {
    this.res.end('Hello ' + this.req.user.username);
  }
  else {
    fs.readFile('index.html', (function(self) {
      return function(err, data) {
        if(err) {
          self.res.writeHead(404);
          self.res.end();
          return;
        }
        self.res.writeHead(200, {'Content-Type': 'text/html'});
        self.res.end(data);
      };
    })(this));
  }
});

/**
 * Here the API to fipassport.authenticate is the exact same as it would
 * be fore passport.authenticate.  It is just a simple wrapper around that
 * function.
 */
app.router.post('/login', fipassport.authenticate('local', {
  successRedirect: '/',
  failureRedirect: '/login'
}));

// Start our server at port 3000.
app.start(3000, function(){
  console.log('HTTP Server started on port 3000');
});
{% endcodeblock %}

Happy Authenticating...