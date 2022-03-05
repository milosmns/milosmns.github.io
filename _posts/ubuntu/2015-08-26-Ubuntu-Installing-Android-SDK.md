---
layout: post
title: Ubuntu · Installing Android SDK and SDK Tools
description: An opinionated guide
date: 2015-08-26 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

_Note: This was tested with Android SDKs 8-22 and is probably severely outdated as you read it today. When updating the Android SDK, do it **always** through the Eclipse plugin or Android Studio, and directly through the SDK Manager._

## Prerequisites

First of all, make sure you have updated your system to the latest version (just in case). You can search this site to see how to perform a system update.

You will also need the latest Android SDK with tools and platform tools. If you already downloaded the Android Studio or Eclipse bundle, the SDK will be inside the bundle. You can also download it directly from Google, but it's gonna be more maintenance.

## Setup

What we are doing here is allowing you to access SDK tools from any location when inside the Terminal, and allowing all scripts running under your username to find and use the tools available in the SDK. Let's go.

If you downloaded an SDK from Google, you should first unpack what you downloaded (_Right Click_ → _Extract Here_) or through the command line (more complicated). I put mine in: `/home/uname/dev/android/sdk`. If you downloaded an Eclipse or Android Studio bundle, your SDK will be inside of the downloaded package in the `sdk` folder. Find it.

Whatever the case, remember the location of your SDK because it is extremely important for the next steps.

## Adding to current user’s path

If you are using Sublime Text as your primary editor (I am), you should be able to paste the commands below without any change. If you are using other editors (such as GEdit, Nano, Vim, etc) you need to replace `sublime-text` in all commands with your editor command.

Open your Terminal. Let's edit your profile config file:

```bash
sublime-text ~/.bashrc
```

If your using `z-shell`, you should then edit your profile config in `~/.zshrc` instead.

At the end of file, we should add new directories to the path. Paste your SDK location twice, once with `/tools` and once with `/platform-tools` suffix, like so:

```
export PATH=$PATH:/home/uname/dev/android/sdk/tools:/home/uname/dev/android/sdk/platform-tools
```

Remember, my SDK was extracted to `/home/uname/dev/android`, you should put your own location instead of that.

Save and close. Note that you could define some variables in your profile config and use those instead, but that’s a bit more complex and we’ll skip it for now.

## Applying the changes

There is one more step to do here - you need to re-initialize your Terminal session to apply the changes. You can also log out and re-log in, but it's easier to just run the init script again.

This is how you can re-initialize:

```bash
source ~/.bashrc
```

or shorter:

```bash
. ~/.bashrc
```

You can optionally reboot the machine, but it's almost never necessary.

In case you want to, you can quickly reboot from the Terminal:

```bash
sudo reboot now
```
