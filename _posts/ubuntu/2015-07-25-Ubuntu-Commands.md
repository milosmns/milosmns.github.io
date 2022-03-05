---
layout: post
title: Ubuntu · Entering commands
description: An opinionated guide
date: 2015-07-25 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

Similarly to Windows machines (or Macs), you'll have some sort of a starting menu (or a start bar) on your Linux. On Ubuntu it will be on the left side of the screen by default. You can view some of the frequently used shortcuts in Ubuntu by holding down the “**super**” button. If you’re using a Windows-like keyboard, the button will look like a Start Menu icon, located between the “**Ctrl**” and “**Alt**” OR “**Fn**” and “**Alt**” keys. Check the image below.

{:refdef: style="text-align: center;"}
![image](/images/posts/keyboard-windows.png)
*Windows Keyboard*
{: refdef}

If you’re using a Mac keyboard, your Super key will be the “**Option**” key. Check the image below.

{:refdef: style="text-align: center;"}
![image](/images/posts/keyboard-mac.png)
*Mac Keyboard*
{: refdef}

If you’re using a keyboard that’s been manufactured for Ubuntu, you’ll have a key like the one below to use as a Super key. Check the image.

{:refdef: style="text-align: center;"}
![image](/images/posts/keyboard-ubuntu.png)
*Linux Keyboard*
{: refdef}

If you're connected to a remote server, you'll be already running a Terminal (or another Command Line) window. You can then just type.

### Opening a Terminal window

If you want to open the Ubuntu's main/"lens" menu, you should just tap the Super button once. From there, you can just start typing on your keyboard and you will see that icons are changing as you type. To get the main Terminal window, you should type the word “**Terminal**” and click on the dark icon.

You should see a window open, and an empty colored sheet, with your name and your PC’s name, e.g. **david@red-laptop**, followed by a blinking indicator that allows you to type there. That’s where you can give all your commands. Once typed, commands are sent to the system by pressing the “_Enter_”/”_Return_” key on the keyboard.

#### Pro tips

  * There is a quicker way to open Terminal. From anywhere in the system, (assuming you're on a Windows keyboard) just tap the shortcut **Ctrl + Alt + T**. 

  * Shortcut **Ctrl + C** force-stops the current command, whichever state it is in. Basically this is a kill-switch for commands if they get stuck or take too long to complete. If you type the command `exit`, your Terminal session will end and the window will close.
  
  * If you type the command `clear`, Terminal will clear itself of any previous text.
  
  * If you press the `up-arrow` key from the keyboard, Terminal will type the last used command for you, waiting for “_Enter_”/”_Return_” to execute it.

  * Terminal is sometimes called "Shell", "CMD", "Command Line", "Prompt", “Bash” or “Dash”. These are names for the Terminal environments and not the Terminal program itself, but people use them interchangeably regardless.
