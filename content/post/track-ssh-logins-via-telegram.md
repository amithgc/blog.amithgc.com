---
title: "Track SSH Logins via Telegram"
date: 2023-01-15
description: Track SSH Logins via Telegram
authorbox: true
sidebar: false
thumbnail: "img/ssh.webp"
pager: true
categories:
  - "Development"
  - "Automation"
tags:
  - "AUTOMATION"
  - "CODE"
  - "SSH"
  - "TELEGRAM"
---

If you are a Dev-Ops Engineer, You and Your team may want to keep a track of who is logging in to which Servers/Virtual Machines.

In this article, We will learn how to create a Telegram Bot and write a shell script to send messages to Telegram messenger using the Curl command.

Then you will also use this shell script to send a notification to your Telegram Channel when a SSH login is detected.

---

### Building a Telegram Bot
Bots are **third-party applications that run inside Telegram**. Users can interact with bots by sending them messages, commands and inline requests. You control your bots using HTTPS requests to our Bot API.

To send a message to Telegram group or channel, you should first create your own bot. Just open Telegram, find @BotFather and type `/start`. Then follow instructions to create bot and get token to access the HTTP API.

![](../images/ssh1.webp) ![](../images/ssh2.webp) ![](../images/ssh3.webp) ![](../images/ssh4.webp) ![](../images/ssh5.webp)


- Search for @BotFather and click on “Start” or type “/start”
- Type “/newbot” to start creating a new Bot
- Name the bot. Example, in our case we are naming the bot as “test-ssh-bot”
- You will get a HTTP Access Token (marked in red). Make a note of it, You will have to use it in the shell script.
- Also, Tap on the link “ t.me/sample_test_ssh_bot” to message the bot. Send a test message to the bot.

Congratulations! Now at this point of time, You have a Bot ready.

---

### Creating Telegram Chat Channel


![](../images/ssh6.webp) ![](../images/ssh7.webp) ![](../images/ssh8.webp) ![](../images/ssh8.webp)

Create a new **Channel** and name it as **SSH Channel**. Also add the bot we created in the last step to this channel as a **subscriber**.

After the Channel is created, Send a test message to the channel.

---

### Get the required Details


Now that you have everything ready at Telegram’s side, Lets get the required details to write the Shell Script.

We need 2 things

- Bot Token — We have already got it
- Group Chat ID

Open the following link in any of the 

`https://api.telegram.org/bot<YourBOTToken>/getUpdates`

![](../images/ssh10.webp)

You will see a json response, If you don’t see any data you should send a test chat message in the channel first. **Highlighted** in red is your **Group Chat ID**. Make a note of it, You will have to use it in the shell script.

---

### Shell Script to send a Telegram message

To send a message we could use simple command like

`curl https://api.telegram.org/bot<YourBOTToken>/sendMessage?chat_id=<group_chat_id>&text=<text_message>`

Now, Lets build a Shell Script which can send a message on every SSH

Create file as `/usr/local/bin/notify-on-ssh-login.shin` the server which you want to monitor.

```bash
#!/bin/bash

TOKEN="<BOT_TOKEN>"
ID="<GROUP_CHAT_ID>"
URL="https://api.telegram.org/bot$TOKEN/sendMessage"

if [ "$PAM_TYPE" != "open_session" ]
then
  exit 0
else
  curl -s -X POST $URL -d chat_id=$ID -d text="$(echo -e "Host: `hostname`\nUser: $PAM_USER\nHost: $PAM_RHOST")" > /dev/null 2>&1
  exit 0
fi
```
Give *executable* permission to this file

`chmod 777 /usr/local/bin/notify-on-ssh-login.sh`

Open the file sshd (`vi /etc/pam.d/sshd`) and add the following line

`session optional pam_exec.so /usr/local/bin/notify-on-ssh-login.sh`


### Results
Congratulations!, You are all done. Now when anyone with the SSH Access logs into the VM, You will get a message as below.
Now you can add everyone in you Dev-Ops team to this Group.

![](../images/ssh11.webp)









