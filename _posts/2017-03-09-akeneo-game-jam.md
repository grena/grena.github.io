---
title: "Akeneo Game Jam"
author: grena
layout: post
permalink: /akeneo-game-jam
disqus: http://www.grena.fr/akeneo-game-jam
date: 2017-03-09 18:00:00
path: 2017-03-09-akeneo-game-jam.md
---

At Akeneo, we have a nice recurrent event called the **Akeneo Game Jam**.
If you're not familiar with Game Jams, it's generally a really **short event** (_2 or 3 days_) during which people, **solo or in team**, try to **make a game** around a given **theme** (_picked randomly then voted_).

For now, and as it's quite hard to gather 10 people the same weekend, we decided to do the first editions of the Game Jam on several weeks. This way, everyone can participate, some hours on their free time at home or on weekends. This offers more flexibility. Then, once the due date is over, we invite our collegues for a "demo session" where we can show our games, and it's super funny!

3 Game Jams later, I thought it was sad to "loose" contact of all previous jams and games. The other problem is that it was hard to share the whole Jam result to all curious people through social medias. That's why I decided to create a simple static website to gather all the Akeneo Game Jams information as well as games. You can now play all games we made during the jams! "**victory trumpet sound**"

[https://akeneo.github.io/gamejam/](https://akeneo.github.io/gamejam/)

### How does it work?

The website had to be static, so basically html/css/js to easily be deployed through GitHub with [GitHub pages](https://pages.github.com/). 
Then it had to be easy to "publish" a new game made for the Jam.

So I came up with this solution:

- All game informations are in subfolders of the website
- Each game folder contains `.json` and `.md` files a well as pictures of the game (_they are developers, so filling a `.json` file is easy for them_)
- The JS scripts fetch the `.json` (_with simple `$.getJSON()` calls_) then render it through some [VueJS](https://vuejs.org/) views 

So it's easy for someone to quickly add a game to display on the website:
```
data
├── games
│   └── my-super-game
│       ├── description.md
│       ├── meta.json
│       └── pictures
│           ├── a_picture.png
│           ├── another_one.png
│           ├── and_a_screenshot.png
│           └── amazing.png
└── web stuff, with js, css, html...
```

I just picked [VueJS](https://vuejs.org/) to have a really simple view system. I didn't use this "framework" before starting this project, and I think it's pretty straightforward to have something working quickly. Plus it's really well documented.

That's it! It was fun to set up this nano project in one evening. Feel free to browse the [Akeneo Game Jam website](https://akeneo.github.io/gamejam/) to explore games made during it, see you!
