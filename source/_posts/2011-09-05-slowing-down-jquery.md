---
layout: post
title: "Slowing down jQuery"
tags:
- ajax
- development
- javascript
- jquery
- slow
- tricks
status: publish
type: post
published: true
meta: {}
---
I wanted to work on adding a nice 'loading...' effect to my application,
of which I have little access to its server code. I needed to find a way
to slow down my AJAX calls, so I can see the effect and tweak it in my
browser.

Unfortunately, AJAX is too fast on a local environment, and I couldn't
find anything about slowing jQuery down (all Google found were 'jQuery
script too slow' question pages).

Fortunately, a co-worker and I figured that we could take advantage of
the new [jQuery Deferred
objects](http://api.jquery.com/category/deferred-object/).  
I added this line to a function that wraps AJAX calls:

https://gist.github.com/1194488

And it worked like magic.

It merges the original AJAX's promise along with something that takes
time (i.e. the 3s `fadeOut` animation), and then uses a [deferred
pipe](http://api.jquery.com/deferred.pipe/) to make the promise only
return the original AJAX result.

Cool!

You use it like this:

https://gist.github.com/1194515
