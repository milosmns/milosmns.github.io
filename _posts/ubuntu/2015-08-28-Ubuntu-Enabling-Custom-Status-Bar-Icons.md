---
layout: post
title: Ubuntu · Enabling custom status bar icons
description: An opinionated guide
date: 2015-08-28 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

By default, not all programs are allowed to show their icons in the top status bar (also sometimes called menu bar). We can fix that.

First of all, make sure you have the latest system updates, just in case. You can find how to do that by doing a quick search for system updates right here on the site.

When done, go to [Florian's site](http://www.florian-diesch.de/software/unsettings) to install **Unsettings**. You might be able to find it in the **Software Center** too.

When installed, you can open the Lens menu, and look for **Unsettings**. Open it, and go to the **Panel** menu. You will see an editable list of items there.

On the top of that list, add the following line:

```bash
all
```

To apply the changes, click on the cogwheel icon. I know, it makes no sense that the cogwheel icon means “save”. 😃

Finally, close the program, and try opening a program that uses the status bar (for example, _Skype_ does it). Skype’s icon should now appear near the clock and date.
