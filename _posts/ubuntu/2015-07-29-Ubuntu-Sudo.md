---
layout: post
title: Ubuntu · About SuperUser (sudo)
description: An opinionated guide
date: 2015-07-29 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

When you log into your Ubuntu OS, you can see your files after clicking on the folder icon (that’s when you go to your Home folder, by default). Every user on the machine has their own private Home folder.

Having a multi-user functionality makes a system more user-friendly. Other than your own user, there can be (almost) infinitely many users on a system -- but there is only one user that can’t be removed. Not easily anyway. That user is the absolute system admin, called `SuperUser` or `root`. If you use the Terminal, your username will be presented at the beginning of the line, something like this:

```console
username@pc-name $
```

If you open the Terminal from your user interface, by default it will be opened "as the current user", i.e. yourself. If you need extra privileges -- like when you’re installing a program, app, or modifying some protected files -- you need to have that administrator's access level. Even though you may be _the only user_ on your machine, it's still required. That’s just how a Unix system works.

To assume administrator rights on your Unix system, type the command:

```bash
su
```

On Ubuntu, you need to type:

```
sudo su
```

That `sudo` command allows you to run the following `su` command as a root user (administrator).

The Terminal will immediately ask you for an administrator password. You will not see the characters on the screen while you type the password, but they’ll be received. So basically whenever something fails due to the lack of permissions, the simplest fix is to try to run it again with a `sudo` command in front.
