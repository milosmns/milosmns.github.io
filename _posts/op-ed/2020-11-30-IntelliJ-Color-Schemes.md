---
layout: post
title: Color Schemes in IntelliJ IDEA (Light and Dark)
description: A freebie - sharing my color configurations for IntelliJ IDEA editors (code) and the related family of IDEs
date: 2020-11-30 15:00:00 +0100
image: '/images/posts/light-dark.jpg'
tags: [op-ed, mac, windows, linux, ide, theme]
featured: false
---

#### Motivation

I use Dark and Light modes equally in all my editors and the OS -- **Light** mode during the day and **Dark** mode during the evening and night.

My thinking here is simple: if the app developers decided to support both themes, to put in the extra work, I'll use both modes to maximize their impact. 🙂

I'll be referring to IntelliJ IDEA most of the time, but almost any JetBrains IDE should behave the same way. The color schemes for code I use with **Darcula** and **Default** themes are heavily customized, so I thought my color configurations are worth sharing. They're freebies, see below.

## IDEA 2020.3 Updates

With IntelliJ IDEA's `2020.3` update, I now see a setting to automatically sync the theme with the OS theme. Yes! If you don't have it, my suggestion is to go grab the latest IDE version and check it out.

{:refdef: style="text-align: center;"}
![Theme Sync](/images/posts/ide-themes-sync.png)
*OS theme sync*
{: refdef}

## Font Ligatures

Here's a quick legibility tip: if you want to use [Font Ligatures](https://en.wikipedia.org/wiki/Ligature_(writing)) (try it out if you haven't), one of the best fonts that supports them is [JetBrains Mono](https://www.jetbrains.com/lp/mono).

I turned this on in my IntelliJ IDEA through **Preferences** → **Editor** → **Font**, and toggled **Font Ligatures**. Some examples are marked using green.

{:refdef: style="text-align: center;"}
![Font Ligatures](/images/posts/ide-ligatures.png)
*Font ligatures on the bottom*
{: refdef}

## Color Schemes

Schemes? Themes? It's confusing.

  - **Themes** refer to window coloring, buttons, icons, etc.
  - **Color Schemes** refer to code and editor coloring, like class names, comments, basic types, etc.

Whether you're using **Darcula** (dark) or IDEA's **Default** (light) theme, your code editor is set up with a default **code** color scheme for that mode. You can spice up your editor appearance. 🔥

My personal dark and light color schemes (for code editors) are available for download as a `.zip` at:

  - [This Gist page](https://gist.github.com/milosmns/0d06835368a0309e689284325fc3f591)

Unzip after downloading. To import each of them, use the following menu:

{:refdef: style="text-align: center;"}
![Scheme Import](/images/posts/ide-import-schemes.png)
*Importing color schemes*
{: refdef}

The look you'll be getting after importing those:

#### Light

{:refdef: style="text-align: center;"}
![Scheme Light](/images/posts/ide-scheme-light.png)
*Light sample*
{: refdef}

#### Dark

{:refdef: style="text-align: center;"}
![Scheme Dark](/images/posts/ide-scheme-dark.png)
*Dark sample*
{: refdef}
