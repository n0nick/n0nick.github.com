---
layout: post
title: ! 'GSoC Journal: Weeks 1-2'
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
With the first 2 weeks of the GSoC coding period over, I thought I'd post about what I've been up to so far.

The start of the coding period took me by surprise. I had to learn about it from a post in the [Google Open Source blog].  
I had to re-adjust and flex my schedule to get into working mode, and that wasn't too easy. That's why I'm a bit late with my progress, compared with the timeline I described in [my application]. Nothing that I won't be able to fix later on, though :)

So in the past 2 weeks I was able to:

* Read through some of the [Pygame source], study the basics that get it going.
* Specifically read through [sprite.py] to understand the current state of the sprites system.
* Set up my development environment so that it actually runs the framework and tests successfully.
* Read through most of [Making Games with Python &amp; Pygame], going over the examples code.
* Checked out a few of the [example games], playing around with their source code.
* Studied the `DirtySprite` and `LayeredDirty` classes and their use case.
* Wrote a [DirtySprite and LayeredDirty tutorial]. This was *extremely* helpful in learning to use the feature. Great idea from mentor illume.
* Sent a [Call for Suggestions] to the mailing list regarding my planned features list for the sprite classes. Got tons of helpful feedback from the community.

The last step helped me compose the following first draft of a sprites system features list:

1. Better positioning, using float values.
2. *Anchor points*.
3. Visual Attributes:
     - Rotation angle
     - Scale
     - Crop rectangle
     - Visibility
4. *Smarter layers system*.
5. *Aggregated sprites*.
6. *Sprite picking*.
7. Automated "dirty" rendering.
8. Encapsulating the Collision Detection code.
9. Optional: Animation? Events?

Again, this is just a first draft and all of the items are still in discussion and under consideration.   
If anybody that's reading this here has any ideas for new features or notes on any of the items here, please feel free to write to me, either here, in the mailing list or via email.

### What's next?

As a lesson from last year's GSoC, that I also had to start while a semester was still going, I decided on a little system:   
Every weekend, after summing up what I've been up to so far (i.e., this post) - I will decide on tasks for the next week in a specific format: A list of 4-5 minor tasks and one major task.   
This way, I'll be able to finish the small tasks during the week, when I get back home from school or work. The large task would be done during the weekend.

So, this week I'll:

1. ~~Blog about the 2 weeks and what's next.~~
2. Research some of the features from the list (italic above; items 2, 4, 5, 6);
     - What exactly is required?
     - How is it done in other libraries?
     - How should we do it?
3. Weekend task: Start writing a paper defining the sprite project work, describing the features that would be implemented.

Have a nice week!

[Google Open Source blog]: http://google-opensource.blogspot.com/
[my application]: http://www.google-melange.com/gsoc/proposal/review/google/gsoc2012/n0nick/28002
[Pygame source]: https://bitbucket.org/pygame/pygame/src
[sprite.py]: http://www.pygame.org/docs/ref/sprite.html
[Making Games with Python &amp; Pygame]: http://inventwithpython.com/makinggames.pdf
[example games]: http://www.pygame.org/docs/ref/examples.html
[DirtySprite and LayeredDirty tutorial]: http://dotfile.n0nick.net/quick-dirty-using-pygames-dirtysprite-layered 
[Call for Suggestions]: http://www.mail-archive.com/pygame-users@seul.org/msg16858.html
