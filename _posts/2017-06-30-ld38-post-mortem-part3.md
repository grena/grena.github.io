---
title: "Ludum Dare 38, the Post Mortem (part 3): Sunday"
author: grena
layout: post
permalink: /ld38-post-mortem-part3
disqus: http://www.grena.fr/ld38-post-mortem-part3
date: 2017-06-30 16:00:00
path: 2017-06-30-ld38-post-mortem-part3.md
---

> This post is the third and **last** of the post mortem of [Pod2000](https://ldjam.com/events/ludum-dare/38/pod2000), our submission for the Ludum Dare 38. You may want to read the [first part](http://www.grena.fr/ld38-post-mortem-part1) and [second part](http://www.grena.fr/ld38-post-mortem-part2) before reading this :)

## Personal note about the Sunday
I feel like there was a **small demotivation in the team**. It’s the second time I do the Ludum Dare, and I already had the same feeling. I think it can be explained easily: the hype of the first day is gone, the main engine and **80% of visible work is done**. 

These last “20%” are mentally hard to accomplish, because it looks like we don’t achieve as many work as the Saturday (which is wrong obviously). However these last “20%” are super important to “polish” the game. But as a player, it’s clearly what distinguishes 2 games in a game jam, in my humble opinion.

## 10h00
Now that we had a very simple basic gameplay, we needed to improve this prototype : add more narrative content (biome description, booting text of the computer…) to bring more life into the game.

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p3-gildas.jpg" class="img-thumbnail ">
    <span>Gildas, working on improving some commands (potato quality edit)</span>
</div>

With that, we decided to improve commands the player can enter in the console and implemented LED feedback system when player successfully builds a module.

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p3-led-system.png" class="img-thumbnail ">
    <span>The LED system, that notifies the user he built a module.</span>
</div>

On audio side, Baptiste made the introduction music we hear for the 2 pictures cinematic! \o/

## 17h00
Mylène virtually joined us (she stayed remote!) to draw the nice pixel art picture of biomes we can see from the planet. It was nice to discover them one by one as she sent them.

<div class="img-legend">
    <img style="display: inline !important;" src="/assets/img/posts/ld38-p3-forest.png" class="img-thumbnail ">
    <img style="display: inline !important;" src="/assets/img/posts/ld38-p3-snow.png" class="img-thumbnail ">
    <span style="display: block !important;">Pixel art biomes, aka pictures sent by VJ-Net42, by Mylène Larnaud.</span>
</div>

Baptiste continued to work on several biomes sounds.

At this step of the development, we **still only have one ending!..** It was a bit sad and the game was missing something, it was too easy to complete and we wanted to reward the player for exploring the planet.

## The 2 endings [SPOILER]
So we discussed about that and then found this idea of having 2 endings depending on your actions on the planet. 

### The corporation ending
In Pod2000, you play an agent belonging to a huge corporation that exploits planets. To exploit a planet, you need to install modules to extract oil, refinery, etc. If you blindly install all modules, you just end your mission and see the planet going red, starting to be exploited. VJ-Net42 just stays on the planet, forever, until the planet will be destroyed.

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p3-corporation.jpg" class="img-thumbnail ">
    <span>When leaving the planet on corporation ending, the planet looks a bit red.</span>
</div>

### The exploration ending
If you explore enough biomes on the planet, you’ll find an alien artefact. When used, it hacks your pod, starts your engine and makes you leave the system. Aliens will take care of the robot, as he’s not an enemy to them.

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p3-artefact.jpg" class="img-thumbnail ">
    <span>On exploration ending, the planet is still blue, untouched, as the exploitation has not begin.</span>
</div>

We were really happy to have this, it gives the game more depth. Technically, adding a new ending was not so hard with the engine we had. The hype was here again, FIRE!


## 20h45
At this time, we implemented the last command the player can type in the terminal: “archive”. You can use it to hear or see again your explorations of the planet.
 
The second ending was in progress.

## 23h00
The last things! We were quite ready to ship, Pierre made us the shiny grunge logo

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p3-logo.gif" class="img-thumbnail ">
    <span>Pod2000 logo, made by Pierre with Blender</span>
</div>

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p3-fallout.png" class="img-thumbnail ">
    <span>Yes, we liked the grunge logo of Fallout, and it was clearly an inspiration <3</span>
</div>

With Geoffrey, we tried to improve the “undock” command (as it’s one of my favourite moment in the game). So we implemented (in a very dirty way haha) the shaking and blinking of the screen when VJ-Net42 undocks from your pod, but we were really happy of the result!

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p3-shake.gif" class="img-thumbnail ">
    <span>We simulate the extinction of light, so that the screen is the only source of light (green)</span>
</div>

<div class="img-legend" style="margin-top: 30px;">
    <img src="/assets/img/posts/ld38-p3-mask.png" class="img-thumbnail ">
    <span>The trick here is just to render the picture with a dirty-green filter and then quickly pop this picture above the other</span>
</div>

## The end
After this, we shipped the game on the Ludum Dare website, it’s was over. We were tired but very happy of the result, we wanted to set up a dark mood of isolation, and the huge work made by Baptiste on the audio environments helpt a lot. So yes, working with that many people in 48h is easily doable and fun, as it brings so many ideas & solutions. 

I hope this post-mortem wasn’t boring, thanks a lot for reading, and see you for the 39th Ludum Dare! <3
