---
title: "Ludum Dare 38, the Post Mortem (part 2): Saturday"
author: grena
layout: post
permalink: /ld38-post-mortem-part2
disqus: http://www.grena.fr/ld38-post-mortem-part2
date: 2017-05-18 16:00:00
path: 2017-05-18-ld38-post-mortem-part2.md
---

> This post is the second of the post mortem of [Pod2000](https://ldjam.com/events/ludum-dare/38/pod2000), our submission for the Ludum Dare 38. Go [here](http://www.grena.fr/ld38-post-mortem-part1) to read the first part :)

## Saturday morning rimes with brainstorming
As we decided to try the compo mode of the jam (_48h & no pre-made assets_), we knew that we 
quickly needed to define a theme and a gameplay (_to give some times for assets creation_). 
So from 10am to 12am, we noted all ideas and themes, as they were coming! 

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p2-board.jpg" class="img-thumbnail ">
    <span>White board & post-it, reaaaally nice to bootstrap ideas! (Gildas & Baptiste)</span>
</div>

Here are some ideas we had during this crazy brainstorming:

- A game in which you play small people / creatures **inside a coffee machine**. You receive orders that you should fulfill by activating different parts of the coffee machine (Diner Dash like game)
- A game where we can **influence a small planet with external factors**: weather, geological transformations, biome control
- Something with **ants**...

We loved the way we could influence on a planet with indirect actions. So we quickly dug into this idea. 

## Phaser & Typescript
We decided to go for a simple stack by using [Phaser](http://phaser.io) (a Javascript / Typescript game engine). 
Nidup had a nice custom boostrap to setup Phaser projects, which avoid us to have to configure 
Typescript build, configuration, etc… something we definitely don’t want to spend time on during a 
Game Jam :D

## 14h30
Once we found the basic gameplay of Pod2000, we quickly started to develop the main brick of the game, aka. the terminal ! At 2pm, we started to have a very basic terminal (no GUI, just ready in the code). Meanwhile, Pierre draw the interface of the game:

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p2-computer-drawing.jpg" class="img-thumbnail ">
    <span>The very basic interface of the game, drawn by Pierre.</span>
</div>

## 18h30
For like 4 hours, we plugged the terminal engine with graphic elements (the input & the textarea, as we use Phaser). Plus we already had the first very basic commands!

_Fun fact_: we lost some time trying to use a Phaser input component, which was very complicated. 
Finally, as we worked in the web browser, we decided to play it raw and use simple `<input>` and `<textarea>` 
elements :3

## 20h00
> “Hey guys, I’ve recorded all keyboard sounds, could you plug it into the game?”

**HELL YEAH**. Baptiste secretly put himself in a room for several hours with… something:

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p2-thomsonMO6.jpg" class="img-thumbnail ">
    <span>A freaking Thomson MO6, where all the keyboard sound in Pod2000 come from (banana for scale)</span>
</div>

32 key sounds, 8 spacebar sounds & 8 enter key sounds ([available here](https://github.com/nidup/ldjam38/tree/master/assets/sounds/keyboard)). That’s how _crazy_ he is. Once we plugged the typing sounds in the game, we really CAN’T stop playing with these haha!

It was time to celebrate with some barbecue & beers :)

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p2-geoffrey-adrien.jpg" class="img-thumbnail ">
    <span>Beer time (Geoffrey & Adrien)</span>
</div>

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p2-barbecue.jpg" class="img-thumbnail ">
    <span>THE FIRE (Baptiste & Gildas)</span>
</div>

## 22h00
Once we were full of food, we thought about adding more narrative elements plus having the main story making sense. 

As this step of the development, the game was a bit poor, the player just had to build 4 modules 
to win the game. Ahem. But at least **we had the game mechanic**, now we had to bring some life to this 
planet and **give feeling to the player**.

As a bonus, we added the nice screen scanning effect, a modified version of [this WebGL effect](http://glslsandbox.com/e#18578.0).

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p2-screenfx.png" class="img-thumbnail ">
    <span>How we handle the screen FX.</span>
</div>

## 00h20
For more than 2 hours, we refactored (yes, during a Game Jam hahah) the way we displayed messages to the terminal. We have indeed 3 outputs:
- The Terminal screen itself
- The Monitor screen (to display pictures)
- The Audio soundspeaker

With this refactor, we could simply play a sound, plus show an image & some text in the terminal, we were ready to add more content :)

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p2-baptiste.jpg" class="img-thumbnail ">
    <span>Working on the pod sound ambient… (Baptiste)</span>
</div>

Baptiste continued his work on sound, now we had the nice computer boot sound and buzz errors when the command was invalid!

## 02h15
The last 2 hours of the day were interesting. When it’s becoming late, it’s easy to fall in the trap of “refactoring” and “implementing this oh-so-crazy idea that could be great”. But it’s **NEVER a good idea**!

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p2-midnight.jpg" class="img-thumbnail ">
    <span>2am, team becomes to be a bit tired, but we were happy to have the very basic gameplay (Geoffrey, Nicolas, Gildas)</span>
</div>

As you can see on the picture above, we practiced time to time the **mob-programming** on a huge screen. It allows to dig a subject with multiple brains and avoid deadlock on complex topics, it helped us a lot :)

We added some narrative elements and the ability to finally load an image on the small monitor. That was it. The game was ready for more content!

Here is a potato quality video of what the game looked like at the end of the first day, at 50% of the game jam:

<iframe width="560" height="315" src="https://www.youtube.com/embed/VXkLdRRRYWc" frameborder="0" allowfullscreen></iframe>

As you can see, we still had the low quality 3D rendered pod computer ^^

Well, that’s it for the first of the 2 days, in the next post, we’ll see how we managed to finish and polish the game the most we can, plus by adding an alternative end to the game. See you!
