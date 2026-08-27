---
layout: post
title: Ubuntu · Minimize apps on icon click
description: Enable click-to-minimize behavior for Ubuntu Unity launcher icons by adding the Minimize Unity 7 PPA and upgrading the required packages.
date: 2015-08-29 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

I miss some of the Windows behaviors, one of which is clicking on the app icon to minimize it. To have a similar behavior to that on Ubuntu, you need quite a few software packages installed.

Be careful though. The only way I found was to let the OS upgrade itself based on the new packages available, which triggers a wider distribution upgrade. Make sure to backup beforehand.

```bash
sudo add-apt-repository ppa:zxcq14/minimize-unity-7
sudo apt-get update
sudo apt-get dist-upgrade
```

A reboot may be needed afterwards:

```bash
sudo reboot now
```
