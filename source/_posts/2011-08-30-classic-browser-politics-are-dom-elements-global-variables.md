---
layout: post
title: "Classic browser politics: Are DOM elements global variables?"
tags:
- browsers
- client side
- firefox
- html
- html5
- javascript
- web
- webkit
status: publish
type: post
published: true
meta: {}
---
This is hilarious:

A co-worker noticed something strange happening in his Chrome browser:
Every element in an HTML page that has an `id` attribute gets attached
as a member of the global `window` object!  
I checked and it happens in my Safari as well. A bit of googling led us
to [the answer at
StackOverflow](http://stackoverflow.com/questions/3434278/ie-chrome-are-dom-tree-elements-global-variables-here):

> What is supposed to happen is that ‘named elements’ are added as
> apparent properties of the `document` object. This is a really bad
> idea, as it allows element names to clash with real properties of
> `document`.
>
> IE made the situation worse by also adding named elements as
> properties of the `window` object. This is doubly bad in that now you
> have to avoid naming your elements after any member of either the
> `document` or the `window` object you (or any other library code in
> your project) might want to use.

...

> Opera copied IE, then WebKit joined in, and now both the
> previously-unstandardised practice of putting named elements on
> `document` properties, and the previously-IE-only practice of putting
> them on `window` are
> [being](http://dev.w3.org/html5/spec/Overview.html#dom-document-nameditem)
> [standardised](http://dev.w3.org/html5/spec/Overview.html#named-access-on-the-window-object)
> by HTML5, whose approach is to document and standardise every terrible
> practice inflicted on us by browser authors, making them part of the
> web forever. So Firefox 4 will also support this.

This is such a funny turn of events. And a great metaphor for how these
inner decisions are made in browser politics.
