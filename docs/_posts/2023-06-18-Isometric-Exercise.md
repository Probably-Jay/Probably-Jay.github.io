---
title: "Isometric Exercise"
date: 2019-05-27
last_modified_at: 2023-06-11
categories:
  - Project-Postmortems
tags:
  - Game
  - Game-Jam
  - C#
  - Unity
header:
  overlay_image: /assets/images/Projects/Isometric-Exercise/Opening.jpg
  teaser: /assets/images/Projects/Isometric-Exercise/Iso/Iso-tight.png
  og_image: /assets/images/Projects/Isometric-Exercise/Iso/Iso-tight.png
  caption: "Opening of Isometric Exercise"
  actions: 
   - label: "Play Isometric Exercise"
     url: "https://probablyjay.itch.io/isometric-exercise"
excerpt: "Inspired: What would our world look like if you were flat?"
tagline: "Inspired: What would our world look like if you were flat?"
photo1:
  - url: "/assets/images/Projects/Isometric-Exercise/wobbler.png"
    image_path: "/assets/images/Projects/Isometric-Exercise/wobbler.png"
    alt: "The Wobbler lighting up a room"
    title: "The Wobbler (sourcegaming)"
photo2:
  - url: "/assets/images/Projects/Isometric-Exercise/open.gif"
    image_path: "/assets/images/Projects/Isometric-Exercise/open.gif"
    alt: "The view from the start of the game"
    title: "Opening of Isometric Exercise"

gallery1:
  - url: /assets/images/Projects/Isometric-Exercise/up2.gif
    image_path: /assets/images/Projects/Isometric-Exercise/up2.gif
    alt: "Rising with the effect"
    title: "Rising with the effect"
  - url: /assets/images/Projects/Isometric-Exercise/up3.gif
    image_path: /assets/images/Projects/Isometric-Exercise/up3.gif
    alt: "Rising without the effect"
    title: "Rising without the effect"
---
# Isometric Exercise
> *"Perhaps this will change your perspective."*

This was another little game jam I did along with friends *Emelia Fernandez* and *Matt Stark*. 
We had just come back from the V&A's [Design/Play/Disrupt exhibition](https://www.vam.ac.uk/exhibitions/videogames),
and were completely enamoured with Robin Baumgarten's [*The Wobbler*](https://wobblylabs.com/projects/wobbler).

*The Wobbler* is designed to be a 1-Dimensional dungeon crawler, 
with a single input moving the player (a point of light) up and down a single strip of LEDs. 
The controller being an old spring doorstop, apparently inspired by a video of a cat playing with one.

{% include gallery id="photo1" %}

Baumgarten managed to squeeze a huge amount of interaction out of this incredibly simple set-up. Playing with this one dimensional character,
we wondered how a game like this would look in first person. And so the idea for Isometric Exercise was born.

We settled on a 2D character exploring our 3D world. Our character would view a single 1D slice of the world, much as we view a 2D plane, gaining depth perception from
perspective and context clues. We took this band of pixels and stretched them across the whole screen, and the results... were really quite good.

{% include gallery id="photo2" caption="The opening of Isometric Exercise" %}

It's surprisingly readable. To my eyes at least. You can see an opening between two walls that stretches off into another room, which 
contains some large red object. As you move through, your view of the world changes just as it would in 3D.
I think Matt's shader is doing a lot to help here, with the emphasised black-line edges and distance fog you'd be
forgiven for not noticing that there is only one dimension information in the pixels on your screen. 

The real mind bending part of the experience is when we give you the ability to move through the third dimension.
While all that is happening is the line of pixels you can see is sweeping up and down, it looks like the
world is shifting and changing in a way slightly beyond your comprehension.

{% include gallery id="gallery1" caption="Comparison of the rising effect with and without the shader active." %}

We designed evey aspect of the level to make moving in this way dynamic and striking. The wall texture changes,  


