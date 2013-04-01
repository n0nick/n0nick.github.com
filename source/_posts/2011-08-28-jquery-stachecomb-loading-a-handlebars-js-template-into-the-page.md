---
layout: post
title: "jQuery stacheComb: Loading a Handlebars.js template into the page"
tags:
- client side
- handlebars.js
- javascript
- jquery
- plugin
- templates
- web
status: publish
type: post
published: true
meta: {}
---
[Handlebars.js](http://www.handlebarsjs.com/) is great.

It's a superset of the brilliant
[mustache](http://mustache.github.com/) template engine, written
especially for Javascript and with client-side in mind, and it provides
a very elegant and organized way for using templates on a rich
client-side application. If you're looking for a template engine, I
highly recommend looking into it.

I got to know it working on a previous application that I built around
the uberkool [Sammy.js](http://sammyjs.org/) framework. Among all of its
features, Sammy lets you announce you're going to use a template for the
main element and it would handle the loading and inserting of template
content into the page.

Now, working on another app that's not using Sammy, I needed to get this
specific functionality, with a touch of improved performance;  
I needed a plugin that, like Sammy, would make an AJAX request for the
template file if it doesn't have it loaded yet, but additionaly in the
production environment, I could just add these templates to the main
markup (i.e. in a build script) and the plugin would use them without
another request.

This was fairly easy but I thought I'd share the result: The jQuery
**stacheComb** plugin.

{% gist 1176566 %}
