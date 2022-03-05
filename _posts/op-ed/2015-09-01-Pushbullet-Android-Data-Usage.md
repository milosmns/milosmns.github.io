---
layout: post
title: Pushbullet on Android · Data Usage Alert
description: How Pushbullet was abusing my device and my network to send and receive ridiculous amounts of data
date: 2015-09-01 15:00:00 +0100
image: '/images/posts/server-rack.jpg'
tags: [op-ed, android, apps, ux]
featured: false
---

**[Pushbullet](https://www.pushbullet.com)** is an Internet service that allows you to sync your phone’s notifications to your desktop computer (and even to other mobile devices), send SMS messages from your desktop, and share links/text/images from one device to another. It has been one of my favorite apps.

I’ve been using Pushbullet for months, but now I noticed something and have to say that I'm concerned about the amount of cellular data this app uses on my phone. Here is the screenshot from my app:

{:refdef: style="text-align: center;"}
![App Config](/images/posts/pushbullet-app-config.png)
*Pushbullet App Configuration*
{: refdef}

And here's the main app:

{:refdef: style="text-align: center;"}
![Main App](/images/posts/pushbullet-main-app.png)
*Pushbullet Main App*
{: refdef}

As you can see, there's nothing extraordinary going on there. I started having concerns when I (accidentally) went into data usage for Pushbullet to see what caused the system warning... and I was surprised to find that Pushbullet was in the first place in terms of data usage, with a whopping 51 MB of data in just 15 days! That’s crazy, right?! Apps don't waste that much data nowadays...

{:refdef: style="text-align: center;"}
![Shock](/images/posts/reaction-shock.gif)
*My reaction, more or less*
{: refdef}

Here's the screenshot from the cellular usage panel:

{:refdef: style="text-align: center;"}
![Cellular Usage](/images/posts/pushbullet-cellular.png)
*Cellular usage*
{: refdef}

Wi-Fi usage is even worse:

{:refdef: style="text-align: center;"}
![Wi-Fi Usage](/images/posts/pushbullet-wifi.png)
*Wi-Fi usage*
{: refdef}

#### Next steps

I’ve written an email to their team to see what’s going on. Being an engineer myself, I could easily sniff out what data it’s transmitting (and where), but I’ll wait the official explanation from the developers...

Synchronizing a few lines of text across 3 devices I use shouldn't accumulate to around 220 MB of data. Something is fishy here, and if I don’t get any updates soon, I’ll post the sniffed data at a later date.

Best of luck with investigations!
