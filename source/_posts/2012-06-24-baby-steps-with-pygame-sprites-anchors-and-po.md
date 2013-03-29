---
layout: post
title: Baby steps with Pygame sprites (Anchors and positioning done!)
tags:
- gsoc
- gsoc2012
- journal
- pygame
- python
- sprite
status: publish
type: post
published: true
meta: {}
---
It has been pretty difficult getting things done in the past week or so, for various reasons (excuses include my birthday, the start of the finals period and some pressure at work).

Initially I was trying at doing unit tests for my [planned sprites work][1], in the [TDD][2] tradition. This proved to be a major creativity block for me, I'm guessing mostly because I'm not too experienced with writing tests.  
So eventually, I decided to take another approach and just get stuff done in a way that could be quickly presented and tweaked.

Today, I managed to get 2 of the planned features ready to be played around with: *Anchor points* and *Better positioning*.  In addition, I have a simple demo app that showcases the use of these 2 features.

[The new `Sprite` class][3] is based on a flat-out copy-paste of the original Pygame `Sprite` class, along with the relevant additions:

* An `anchor` property that will be used for positioning and modifying the sprite. It can be set at any point during the game to either:
  * `ANCHOR_TOPLEFT`
  * `ANCHOR_TOPRIGHT`
  * `ANCHOR_BOTTOMLEFT`
  * `ANCHOR_BOTTOMRIGHT`
  * A custom `(x, y)` tuple relative to the sprite's rectangle coordinates.
* An `anchor_value` method that returns a tuple of the calculated value of the sprite's anchor at a given moment.
* A `position` proprety consisting of `(x, y)` coordinates that, when set, uses the sprite's anchor property to position the sprite on the screen.

The usage of the new features is demonstrated in [the `regions.py` demo][4].  
The demo starts out with a basic grid in which you can move a basketball sprite around with the arrow keys:
![Demo with TOPLEFT anchor](http://f.cl.ly/items/3V3l1a3i381o2f160W2S/Screen%20Shot%202012-06-23%20at%2011.51.01%20PM.png)
During the game, you can use the `a`, `s`, `d` keys to switch between `TOPLEFT`, `CENTER` and `(25, 20)` settings for the anchor, respectively.
![Demo with CENTER anchor](http://f.cl.ly/items/2l1N2j1a3S2p1A2I3Y2T/Screen%20Shot%202012-06-23%20at%2011.51.20%20PM.png)

This is basically it, for now, but I'm pretty satisfied with this small development, as it was integreated easily enough and shouldn't be breaking any legacy uses of the Pygame's `Sprite` classes.

The work is maintained in [the `pygame-sprites` repository][5].  
Please feel free to check out the code and the demo app and send any relevant feedback my way.

I hope to be able to show further progress by the next weekend.


[1]: http://dotfile.n0nick.net/pygame-planned-sprites-work
[2]: http://en.wikipedia.org/wiki/Test-driven_development
[3]: https://github.com/n0nick/pygame-sprites/blob/master/sprite.py
[4]: https://github.com/n0nick/pygame-sprites/blob/master/demos/regions.py
[5]: https://github.com/n0nick/pygame-sprites/
