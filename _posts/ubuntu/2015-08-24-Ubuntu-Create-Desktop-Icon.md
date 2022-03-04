---
layout: post
title: Ubuntu · Creating custom Desktop icons
description: An opinionated guide
date: 2015-08-24 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

It's best to make sure you have the latest system updates first (just in case). You can search on steps to update your system on this site.

When you've updated your system, all latest software repositories should be indexed -- so, you can now install the program that creates desktop icons by typing (or copying) this in your Terminal:

```bash
sudo apt-get install --no-install-recommends gnome-panel
```

When you've installed the Gnome Panel, you can easily create icons on the desktop using the following command:

```bash
gnome-desktop-item-edit --create-new ~/Desktop
```

In the window that immediately opens from there, you can select the name, description, desktop icon, and other properties.
