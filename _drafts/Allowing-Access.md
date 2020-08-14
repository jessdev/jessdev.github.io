---
layout: post
title:  "Allowing Access"
date:   2020-08-13 9:34 PM
categories: Code Docker Discord
---

# Allowing Access
Last time, I built a node based discord bot and I put it into a container so that I could either host it on a different machine in the cloud or on my local docker instance.
This time, the goal is to allow others to allow the bot to access their discord servers without me personally being an admin.
    
And it turns out it's pretty easy.

<button name="button" href="https://discord.com/api/oauth2/authorize?client_id=408450741968306187&permissions=67648&scope=bot">Invite Dad Bot</button>

And that's not particularly interesting. So lets talk about discord's system of authentication and authorization.
