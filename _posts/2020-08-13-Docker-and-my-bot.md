---
layout: post
title:  "Docker and My Bot"
date:   2020-08-13 9:34 PM
categories: Code Docker Discord
---

## Bots & Discord
There are so many bots for discord. Things to track users, help with roles, administration, memes, the list goes on. Discord has a ton of integration capability, it’s fun to play around with. Here’s a list of some the more interesting and useful bots that I have found:
* [Carl Bot](https://carl.gg/) for moderation and automation
* [Member Count](https://membercount.net/) for customisable counters
* [Rythm Bot](https://rythmbot.co/) for 'the best music experience on discord'
* [Scryfall](https://scryfall.com/) for all the Magic the Gathering notifications

So what kind of bot could I possibly build that hasn’t been built yet? The answer is, probably not but I’m going to have fun with something that I absolutely enjoy: puns and dad jokes. 

## Dad Bot
Dad bot is a bot that will yell at you for swearing. Already he's made an enemy of one of my good friends:
![Ah well](/img/Dadbot_01.png)

He's fun, he's punny, he's... most importantly, in demand...?

![I want that bot](/img/i_want_dad_bot.png)

## Dad Bot is in demand
Okay so how to make my bot something that anyone can add? Probably the first step is making it deployable.

Lets' put it into a container.

## How to container
I used the following code to put my silly bot into a container:

```
FROM node

RUN mkdir -p /home/node/dad/node_modules && chown -R node:node /home/node/dad

WORKDIR /home/node/dad

COPY package*.json ./

USER node

RUN npm install

COPY --chown=node:node . .

CMD ["node", "src/bot.js"]

```

let me walk you through the following:

### `FROM node`
I pulled ths container down from docker hub the other day. It's the latest version of the container desinged by [node js](https://hub.docker.com/_/node/). I recomend you read through their read me to fully understand what's in the container.
This will allow me to run node programs in the container without having to install them to the container evnrionment itself.

### `RUN mkdir -p /home/node/dad/node_modules && chown -R node:node /home/node/dad`
This sets up the ownership for the folder to the user 'node.' This is security percaution to limit what the application acount will be able to interact with in the container.

### `WORKDIR /home/node/dad`
This sets the working directory for all commands going forward.

### `COPY package*.json ./` && `RUN npm install`
This step is going to copy the package.json to start building out the node_modules folder.
The install step brings the modules into the container.

### `COPY --chown=node:node . .`
This assigns the node user to owner of the current folder.

### `CMD ["node", "src/bot.js"]`
This sets up the command that starts when the container is deploy. This will actually start up the bot.

## Next Steps
Now that the bot is built and deployed in a docker container the next step is to find a way to allow other users the ability to add the bot to their own server.
