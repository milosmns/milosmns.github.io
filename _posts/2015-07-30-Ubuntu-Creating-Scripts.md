---
layout: post
title: Ubuntu · Creating [Shell] Scripts
description: An opinionated guide
date: 2015-07-30 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

_Note: You'll see that I'm using [Sublime Text](http://www.sublimetext.com/) as my text editor on Ubuntu desktop. You may use [gedit](https://wiki.gnome.org/Apps/Gedit) or anything else really instead. For example, [nano](http://www.nano-editor.org/) is a simple alternative for the Terminal. If you want to install Sublime Text, you can do a quick search for it here._

## What is a bash script?

A **bash** script is, well... a series of Terminal commands typed together in a file, one below the other. The commands are always executed top to bottom, line by line. We often say "bash" and "shell" interchangeably, even though "bash" is a different variant of shell. For the purpose of this post, it's the same thing.

To create a new script, you need to start writing to a file. The easiest for beginners is to use a desktop editor, like Sublime Text.

In the Terminal, type:

```bash
sublime-text myscript.sh
```

If you have a different version of Sublime Text, your command line tool might be called `subl` instead of `sublime-text`, so just replace it if needed.

It’s common for these scripts to have names that end with `.sh`, but you can name it whatever you want. When you’ve opened the empty document, add this as the first line (it basically tells the system which shell to run):

```bash
#!/bin/bash
```

This line tells the location of your Shell executable. It will most likely be in the default location (`/bin/bash`), but you can double-check by typing:

```bash
which bash
```

## Adding commands

Ok, your file now has the executable which to use for running. Below that first line, you can add any command you want (just remember to put them each on a new line). Let’s say we want to write “Hello World” on the screen. The complete file would look like this:

```bash
#!/bin/bash 
echo Hello\ World
```

You can see that the space in "Hello World" is preceded with a `\` character, which allows spaces to be used (note that it doesn’t work for all commands). Another way to print spaces is to put the whole output under double quotes (`"`).

Ok, back to the main thing. Now save that file and (optionally) exit the editor. When you have done that, you have a script file waiting for you to execute it. But the script is not executable yet. The system doesn’t know that this file contains runnable commands by default.

You can enable execution for this file by right-clicking on it from the file browser, then going to Properties, and then modifying the ownership information. Set `allow execution` to **enabled**. Another (faster) way to do it is from the Terminal, like so:

```bash
chmod +x myscript.sh
```

There we go, your script is executable now! You can run it by using the `sh` command, or just by using it’s fully qualified name from the current directory:

```bash
./myscript.sh
```
