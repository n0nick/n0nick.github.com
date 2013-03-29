---
layout: post
title: It's midterms time (already?!)
tags:
- gsoc
- gsoc2012
- journal
- midterm
- pygame
- python
- sprite
status: publish
type: post
published: true
meta: {}
---
I've been very busy in the past couple of months. It's been very educating, very productive - yet the time flew way too quickly!

Outside of [my GSoC Pygame project][1], I have been finishing the semester and stepping into a final tests period which proves to be the hardest yet. I don't remember ever being so exhausted day after day when I get home.

This is the main reason I have to admit that my project doesn't quiet meet the plans to have most of the new Sprite class ready for the midterm evaluations.

Still, I have some good progress to show for, plus I'm fairly sure that after these hectic finals will pass, I will be able to catch up with my plans.

## Let's show off, then.

The [sprites work plan][2] consisted of adding 7 new features to Pygame's [Sprite class][3].  
I wrote about implementing 2 of these (*Anchor points* and *Better positioning*) in my last post, [Baby steps with Pygame sprites][4].

Since then, I have finished implementing 2 more, *Visual attributes* and *Aggregated Sprite*, which I'll describe below, and also wrote most of the underlying code needed for the rest of the features.

You can check out my work in progress, including everything described here, in the [`pygame-sprites`][7] GitHub repository.

### New visual attributes

My `Sprite` class now has several few new properties: `visibility`, `scale` and `rotate`, which control the way the sprite's image is drawn on the screen:

* `visibility` decides whether the image should be rendered  or not. Default is `true`.
* `scale` is a float value determining the ratio between the size of the originally supplied image and the required size on the screen. Default is `1`.
* `rotate` is an integer defining the degree by which to rotate the original image. Default is `0`.

![image](http://cl.ly/26103X3c3k3E12323b0j/Screen%20Shot%202012-07-11%20at%2011.25.45%20PM.png)
![image](http://cl.ly/1s0X0t3b0o2j15023e0y/Screen%20Shot%202012-07-11%20at%2011.25.49%20PM.png)
![image](http://cl.ly/1A3N0N0I1g341N1n0p1r/Screen%20Shot%202012-07-11%20at%2011.25.57%20PM.png)


To implement these attributes I used Python's [`property` notation][6], which allows me to set custom getters and setters for standard class properties.  
In addition to the visual attributes, the sprite's `image` attribute also uses the new notation, so that its custom getter function would return the transformed image, if a transformation is needed.

The visual transformations are done using [`Pygame.transform`][5]'s methods.

### Sprites drawing themselves

In order to support features such as the `visibility` attribute, automatic dirty rendering and others, I changed the way we actually draw the sprites, implementing the [composite pattern][8].  
`Sprite`'s new method `draw` gets a surface as an argument and is responsible to draw the current sprite onto it.  

`Group`'s old `draw` method now uses the group's sprites' `draw` method if it's available. Legacy code is still supported by preserving the old functionality if no `draw` method is found.


### Aggregated sprites

I wrote a new class, `AggregatedSprite`, which extends my `Sprite` class and adds the functionality of holding a list of child sprites and propagating any change to them.  
In a sense, an aggregated sprite is something between a sprite and a sprites group.

The `AggregatedSprite` class has a `sprites` property which holds the list of child sprites. This is a basic Python list which could be modified normally.  
Its `draw` method calls all of the child sprites' `draw`, like a group.

Setting a value to a visual attribute of an aggregated sprite would propagate this value down to all the child sprites.  
This was done in `Sprite` by wrapping the visual attributes' setters with a method that would call an `on_visual_set` callback if one exists.  
`AggregatedSprite` uses this callback to set the make the same attribute change to all the child sprites.

Setting an aggregated sprite's `position` to `(x, y)` would use these values as offsets for all of the child sprites, that is, move them all from their original position by `(x, y)`.

![image](http://cl.ly/2G0b352Q3Q1Q08020w1u/Screen%20Shot%202012-07-11%20at%2011.28.07%20PM.png)
![image](http://cl.ly/2p2B0M0N3u1F1M3E2W0N/Screen%20Shot%202012-07-11%20at%2011.28.15%20PM.png)
![image](http://cl.ly/2s3k1j3M1j2o2d2t3521/Screen%20Shot%202012-07-11%20at%2011.28.26%20PM.png)

### Still missing

I'm still missing 3 features here: *Automatic dirty rendering*, *Sprite picking* and *Smarter layers*.

The move to composite drawing of sprites holds most of the major changes needed for dirty rendering and layered groups, and so there's little work left for these two to be done as well.

I still have to do some research on implementing *Sprite picking*, but I'm sure it will be pretty simple to do.

Also, **tests**.  
Early on, I saw that going full [TDD][9] is slowing me down, and I wanted to get stuff working as soon as possible. So I ditched writing tests until everything is more stable.  
On of my most important tasks once I'm done with my last final would be to write tests for all of my changes.  
This is a big task, but hopefully I could make use code of the demo games I wrote for each feature.

Some other **TODOs**:

1. Anchor points: Use Rect's anchor constants instead of my own.
2. Anchor points: Handle negative values.
3. Positions: Handle float values.
2. Visual attributes: Add *crop rectangle* attribute.
3. Some code cleanup, and way more documentation.

## That's about it.

I can't wait until I'm done with my finals so that I can take this project to the next level (and the one after that, too).

Oh, one more TODO note to self: Blog about the project more. It helps.

As always, feel free to contact me with any question or idea, either here, by email or on #pygame in Freenode.



[1]: http://www.google-melange.com/gsoc/proposal/review/google/gsoc2012/n0nick/28002
[2]: http://dotfile.n0nick.net/pygame-planned-sprites-work
[3]: https://github.com/n0nick/pygame-sprites/blob/master/sprite.py
[4]: http://dotfile.n0nick.net/baby-steps-with-pygame-sprites-anchors-and-po
[5]: http://www.pygame.org/docs/ref/transform.html
[6]: http://docs.python.org/library/functions.html#property
[7]: https://github.com/n0nick/pygame-sprites
[8]: http://en.wikipedia.org/wiki/Composite_pattern
[9]: http://en.wikipedia.org/wiki/Test-driven_development
