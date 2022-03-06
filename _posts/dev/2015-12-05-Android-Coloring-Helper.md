---
layout: post
title: Android Helpers · Coloring utility
description: A free utility to help out with coloring of Android UI elements, drawables and other text and graphics
date: 2015-12-05 15:00:00 +0100
image: '/images/posts/color-pencils.jpg'
tags: [dev, software, android, open-source]
featured: false
---

I wrote a helper class for coloring almost anything in Android (including different types of drawables).

We use it to customize [Bria](https://www.counterpath.com/bria-enterprise/) for our customers in real time. As far as I’ve seen, the most used method is:

```java
Coloring.createBackgroundDrawable()
```

This name is subject to change -- but it gives you a dynamically colored ripple-enabled drawable for Lollipop, OR a dynamically-colored state-list drawable for pre-Lollipop devices.

You can check out the `Coloring.getContrastColor()` method too, if you need to recolor the foreground of a view into a contrasting color versus the background. It's all working dynamically with any color you want as a base.

There's a bunch of other useful stuff inside too! [Here’s the source code](https://gist.github.com/milosmns/6566ca9e3b756d922aa5).

#### Future developments

All of these features, and more, are available now as part of the `Silly Android` library.  
[Check it out here](https://github.com/milosmns/silly-android/blob/master/sillyandroid/src/main/java/me/angrybyte/sillyandroid/extras/Coloring.java)
