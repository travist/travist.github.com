---
layout: post
title: "minPlayer: A minimalistic, plugin-based 'core' media player for the web"
date: 2011-05-15 15:26
comments: true
categories:
---
Today I would like to introduce my latest media player creation. The <strong>[minPlayer](https://github.com/travist/minplayer)</strong>.
The idea behind this media player was that I have a lot of experience building web based
multimedia players, but also noticed that I continually build more and more features into
them based on clients requests.  Because of this, I have decided to create the concept of
a "core" media player whose sole purpose was to only deliver the multimedia experience while
the more complex features would go inside of another media player I created called the [Open Standard Media Player](https://github.com/mediafront/osmplayer).
This allows me to keep the core media functionality slim while still being able to extend onto the minPlayer
class to provide the more advanced features such as Playlists and custom 3rd party integrations.
<!-- more -->

Here is the project page found at
[http://mediafront.org/assets/osmplayer/minplayer/index.html](http://mediafront.org/assets/osmplayer/minplayer/index.html).

<iframe width="100%" height="5000px" frameborder="0" scrolling="no" src="http://mediafront.org/assets/osmplayer/minplayer/index.html"></iframe>
