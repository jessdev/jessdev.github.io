---
layout: post
title:  "Docker and My Bot"
date:   2020-07-25 9:25 PM
categories: Code Docker Discord
header-img: "img/aurelia-material.png"
---


## Bots & Discord
There are so many bots for discord. Things to track users, help with roles, administration, memes, the list goes on. Discord has a ton of integration capability, it’s fun to play around with. Here’s a list of some the more interesting and useful bots that I have found:
* [Carl Bot](https://carl.gg/) for moderation and automation
* [Member Count](https://membercount.net/) for customisable counters
* [Rythm Bot](https://rythmbot.co/) for 'the best music experience on discord'
* [Scryfall](https://scryfall.com/) for mtg

So what kind of bot could I possibly build that hasn’t been built yet? The answer is, probably not but I’m going to have fun with something that I absolutely enjoy: puns and dad jokes. 

## Dad Bot
Dad bot is a bot that will yell at you for swearing. Already he's made an enemy of one of my good friends:
![Ah well](img/Dadbot_01.png)

He's fun, he's punny, he's... most importantly, in demand...?

![I want that bot](img/i_want_dad_bot.png)

## Dad Bot is in demand
Okay so how to make my bot something that anyone can add? Probably the first step is making it deployable.

Lets' put it into a container.

