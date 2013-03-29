---
layout: post
title: ! 'Pygame: Planned sprites work'
tags:
- gsoc
- gsoc2012
- plans
- pygame
- python
- sprite
status: publish
type: post
published: true
meta: {}
---
As a final step before getting busy with refactoring and reorganizing Pygame's sprite classes, I've composed the following short paper describing what I want to get done on each 7 new features planned for this part of the project.

These decisions are based on feedback and suggestions [posted on the discussion list][1] and on the #pygame IRC channel, and also on my private research of other open-source game libraries: [cocos2d][2], [Pyglet][3], [Spyral][4] &amp; [Gloss][5], among others.

This isn't a finalized spec of course, just my way of listing things I want to take care of, and along the way getting feedback from the community.

As always, feel free to contact me with any suggestions or comments.

---

## 1. Anchor points

The `Sprite` object should have an `anchor` attribute, that could be set to either:

* `(x, y)` representing an offset
* One of a set of predefined flags i.e. `CENTER`, `MIDBOTTOM`, `TOPLEFT`, that would remain appropriate even after transformations (scaling, rotating, etc).

The default value would be `TOPLEFT`.

The `anchor` attribute represents a point in the sprite that is used when moving and transforming the sprite.

So for example, if a sprite's anchor is `(10, 20)` and we move it to `(100, 100)` - then in result the anchor pixel would be positioned in `(100, 100)` - meaning in fact, that the sprite's top left coordinates are `(90, 80)`.


## 2. Better positioning

Positioning sprites is currently done by manipulating the sprite's `rect` attribute.

It should be possible to position a `Sprite` object using a tuple `(x, y)` that would have the same effect.  
The tuple would be used in accordance with the sprite's anchor point, as defined above.

The `x` and `y` values should be able to be float values, to allow for varying speeds; For example, moving a sprite by 0.1 pixels every frame and then the sprite would move 1 pixel every 10 frames.  
The actual rendering would use rounded values.


## 3. Visual attributes

A sprite should have several attributes that affect its visual representation, and could be changed dynamically during the run of the game.

* **Visibility**: A boolean to say whether the sprite should be rendered at all. Default is `true`.
* **Scale**: A float defining the aspect between the sprite's original size and what should appear on screen. Default is `1`.
* **Rotation angle**: A float representing the degree the sprite should be rotated with. The rotation is done around the anchor point. Default is `0`.
* **Crop rectangle**: A `rect` value with coordinates relative to the original sprite image, defining the part of the image to render. Default is `((0, 0), (w, h))`, with `w` and `h` being the image's width and height values.

## 4. Smarter layers

A `Sprite` object should have a `layer` attribute, with an integer value representing the layer's z-index.  
This is actually already done in `DirtySprite` and `LayeredUpdate`. We should have it for every sprite.

Rendering sprites should behave as in `LayeredUpdate`, maintaining a list of sprites ordered by their z-index.

## 5. Aggregated sprites

A new class `AggregatedSprite` extending `Sprite` that holds a list of other `Sprite` objects.  

They are all positioned and rendered regularly on the screen, and the `AggregatedSprite` instance could be used to manipulate them together:

* Setting the `AggregatedSprite`'s position to `(x, y)` would use these values as an offset for positioning its sprites.
* Setting a value of one of the visual attributes would use this value to overwrite the same attribute for the sprites.

## 6. Sprite picking

The screen should have a method to pick sprites by coordinates - that is, given a position `(x, y)` it should return a list of all sprites rendered at this point.

* Optional: Pass a flag to only pick visible sprites (`visible = true`).

## 7. Automated "dirty" rendering

All of the sprites and sprite groups should have the dirty rendering functionality of `DirtySprite` and `LayeredDirty`.

Sprites should label themselves dirty automatically as soon as either their position, image, or any other visual attribute were changed.  
This would then cause them to be re-rendered only when necessary.


[1]: http://www.mail-archive.com/pygame-users@seul.org/msg16858.html
[2]: http://www.cocos2d-iphone.org/
[3]: http://www.pyglet.org/
[4]: http://www.eecis.udel.edu/~rdeaton/spyral/
[5]: http://www.pygame.org/project-Gloss-1155-.html

