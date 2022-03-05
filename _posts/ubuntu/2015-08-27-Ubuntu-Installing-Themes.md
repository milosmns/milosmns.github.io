---
layout: post
title: Ubuntu · Installing Themes
description: An opinionated guide
date: 2015-08-27 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

As this is a somewhat advanced topic, you should probably be using Ubuntu for a while before trying to do something like installing new themes. You can download many official Ubuntu themes from all around the web, but these ones below are some of my favorites. And to be clear, there are many themes that I really hate though. 😃

Take a look at this snapshot of the Boomerang theme.

{:refdef: style="text-align: center;"}
![Boomerang Theme](/images/posts/linux-theme.png)
*Boomerang Theme*
{: refdef}

## Themes repository and tweak tools

By running these commands in your Terminal, you will be adding the software repository for theme updates to your system and updating the software availability list from it. It will also install the Gnome Tweak Tool, a multi-purpose settings panel with a UI tweaks plugin.

```bash
sudo add-apt-repository ppa:upubuntu-com/gtk3
sudo apt-get update
sudo apt-get install gnome-tweak-tool
```

## Theme installation

Your repositories are updated now, you can proceed to the theme installation. To install the Boomerang theme, run this:

```bash
sudo apt-get install boomerang
```

Now you need to set it as your current theme.

Go to **Gnome Tweak Tool** (from the Lens menu). Open **Advanced settings**, and choose the theme in there. There is another option -- to set this theme from the Terminal if you prefer that:

```bash
gsettings set org.gnome.desktop.interface gtk-theme 'Boomerang'> gconftool-2 --set --type string /apps/metacity/general/theme 'Boomerang'
```

To set a different variant -- Boomerang-Deux theme -- run this:

```bash
gsettings set org.gnome.desktop.interface gtk-theme 'Boomerang-Deux'> gconftool-2 --set --type string /apps/metacity/general/theme 'Boomerang-Deux'
```

Here are some other themes I also liked:

  - [Mediterranean Day and Night](http://www.webupd8.org/2013/01/beautiful-mediterraneannight-gtk-36.html)
  - [Some other favorites](http://www.webupd8.org/2012/11/8-gtk-36-compatible-themes-available-in.html)
