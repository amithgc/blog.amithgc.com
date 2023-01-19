---
title: "Plex Server Alerts in Telegram Using Node Red"
date: 2023-01-19T20:04:23+05:30
description: Plex Server Alerts in Telegram Using Node Red
authorbox: true
sidebar: false
pager: true
thumbnail: "img/plex1.webp"
categories:
  - "Development"
  - "Automation"
tags:
  - "PLEX"
  - "NODE-RED"
  - "CODE"
  - "DEV-OPS"
---

---

Wouldn't it be nice if you could receive a notification in telegram when a movie starts playing in you [plex](https://www.plex.tv/) server?

![](../images/plex2.webp)

In this Article, We will learn how to setup a bot and make it send notifications when a movie starts playing in plex.

---

### Before you Start
Before you start you would need the following…

- **PLEX Server** : You will need a plex server running in any of your home servers.
> Plex gives you one place to find and access all the media that matters to you. From personal media on your own server, to free and on-demand Movies & Shows, live TV, podcasts, and web shows, to streaming music, you can enjoy it all in one app, on any device.

- **Node-RED Server** : You will also need a Node-RED server running in any of your home server.

> Node-RED is a programming tool for wiring together hardware devices, APIs and online services in new and interesting ways. It provides a browser-based editor that makes it easy to wire together flows using the wide range of nodes in the palette that can be deployed to its runtime in a single-click.

- **Pre-Configured Telegram Bot** : If you don’t know how to create a Telegram Bot, Please refer to my other medium article which explains the details of creating a bot — [link](https://blog.amithgc.com/post/track-ssh-logins-via-telegram/)

> Telegram bots are small programs that can embed in Telegram chats or public channels and perform a specific function. They can offer customised keyboards, produce cat memes on demand, or even accept payments and act as a digital storefront.

---
### PLEX Node-RED Palette
Firstly, you will need to install the Plex Node-RED palette in your Node-RED instance. Open Palettes and search for [`node-red-contrib-plex-ws`](https://flows.nodered.org/node/node-red-contrib-plex-ws) and *install* it.

This palette has the ability to talk to plex server and receive notifications.

![](../images/plex3.webp)

To Configure the plex palette you you need the plex token

---

### Finding the PLEX Token

1. Sign in to your Plex account in Plex Web App
2. Browse to a library item and view the XML for it

![](../images/plex4.webp)

3. Click the XML link at the bottom of the Media Info window.

![](../images/plex5.webp) ![](../images/plex6.webp)

4. Look in the URL and find the token as the `X-Plex-Token` value

![](../images/plex7.webp)

5. Copy this token and save it, We will have to use this token in the next steps.

---
### Setup Plex Palette
Once you have got your plex token, It is now time to setup your Plex Palette in Node-RED. Drag and Drop the Plex Playing Node to the Flow

![](../images/plex8.webp) 

and, Double Click on the Node to Open up the node Settings, In the Server Section, Click to add a new Server. Fill in the ***host*** (ip of your plex server), ***port*** and the ***plex token***.

![](../images/plex9.webp) 

---

### Setting up the Node-RED Flow

Create a flow as below

![](../images/plex10.webp) 

***rbe node*** is added just to make sure that there are no duplicate notifications

![](../images/plex11.webp) 

In the Functions node, Add the following code

![](../images/plex12.webp) 

```javascript
var messageContent = "";

if(msg.payload.includes ("playing")) {
    messageContent = "Now Playing on PLEX: " + msg.session.title + " (" + msg.session.year + ")";
} else if(msg.payload.includes ("stopped")) {
    messageContent = "Stopped Playing on PLEX: " + msg.session.title + " (" + msg.session.year + ")";
}


if(msg.payload.includes ("playing")) {
    
    var id = msg.session.guid;
    id = id.replace("com.plexapp.agents.imdb://", "");
    id = id.replace("?lang=en", "");
    msg.payload = {
        chatId :"<YOUR_CHAT_ID>",
        type : "photo",
        content : "https://m.imdb.com/title/"+id+"/mediaviewer/",
        caption : messageContent
    }
    
    return msg;
} else if(msg.payload.includes ("stopped")) {
    msg.payload = {
        chatId :"<YOUR_CHAT_ID>",
        type : "message",
        content : messageContent
    }
    return msg;
} else {
    return "";
}
```

This JavaScript code will fetch the movie images from **IMDB** and send it via **Telegram**.

---

### Setup Telegram in Node-RED

You will need to configure the Telegram Bot to receive the Notifications, Please refer to the following links to setup a Telegram Bot inside Node-RED

- Create a Bot — [link](https://blog.amithgc.com/post/track-ssh-logins-via-telegram/)
- Add the Bot inside Node-RED — [link](https://flows.nodered.org/node/node-red-contrib-telegrambot)

***Thats it, You are all done!***



