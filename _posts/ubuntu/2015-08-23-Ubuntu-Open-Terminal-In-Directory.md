---
layout: post
title: Ubuntu · Opening Terminal at current directory
description: An opinionated guide
date: 2015-08-23 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

The easiest way to open a Terminal in the current window path is to install a special Nautilus (default file manager) plugin. To do this, go to **Ubuntu Software Center** from the Lens menu, find the search field in the upper right corner of that window. Type:

```
nautilus-open-terminal
```

Install the plugin from the results. After installation, you may need to restart your machine or log in again... or just restart `nautilus` from the Terminal (advanced).

When the plugin is installed, go to any directory and right click on the empty space in its window -- so, not on a folder icon, not on any of the other icons or text. 

You should have an additional option now: `Open Terminal here`.
