---
layout: post
title: Ubuntu · Fixing auto-complete
description: An opinionated guide
date: 2015-08-21 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

If you’re having problems with auto-complete in your Ubuntu Terminal, your locale settings probably got messed up. For some reason, it happens to me quite often.

Anyway, you can fix this issue by typing the following commands:

```bash
sudo locale-gen en_GB.UTF-8
sudo update-locale LANG=en_GB.UTF-8
```

As you can see, I'm using the British locale there. You should change it to a different one that matches your system’s language or your preferences, for example `en_US`, `de_DE`, `fr_FR`, etc.
