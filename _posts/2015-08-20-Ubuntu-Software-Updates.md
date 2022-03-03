---
layout: post
title: Ubuntu · Software Updates
description: An opinionated guide
date: 2015-08-20 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

When you have installed an Ubuntu system, it has some pre-configured update settings built-in. This means that it will [try to] update itself from time to time and you don’t need to touch anything. But as most Ubuntu users do, you probably want some control over this by opening the Update Manager (system program that manages updates) and change some of the settings. Most importantly, you can change which updates are needed (universe, multiverse, main, etc.) and which software distributor sites to contact when searching for updates. Those settings should be in a separate tab of the Update Manager.

More interestingly, you can change the software sites from the Terminal too, and the configuration is located here:

```console
/etc/apt/sources.list
```

When you change the software sources list programatically, for example via the `add-apt-repository` command, or manually by altering the contents inside of the mentioned file, you must update the repository cache. It's kind of a local storage that Ubuntu uses to contact every repository and check which software it contains (as well as package versions).

Simply put, your system has information on what is currently updatable and what is currently available for installation, and this information is stored in a database somewhere on your machine.

When you run the `update` command, you actually update that database of "what is available". You are not updating any software package by running `update`.

So, the full command for updating the software list:

```bash
sudo apt-get update
```

The `apt-get` command is a command from the Ubuntu's package manager and most likely won’t be available on other Linux systems. On newer versions, it's just `apt`.

Anyway, when you have updated that availability database using `update`, you will be able to install and update any programs available in the repositories your system is monitoring. You can install a program using this command:

```bash
sudo apt-get install PROGRAM_NAME_HERE
```

If you need to upgrade **all** programs that are installed on your machine and are available in the repositories your system monitors, you can use this command:

```bash
sudo apt-get upgrade
```

This will actually upgrade the software packages and download new versions of the software you previously installed through `apt`. After running, you should now have all the latest updates. If you want even more programs updated (like system programs and even OS), you can use this command:

```bash
sudo apt-get dist-upgrade
```

This goes without saying... but make sure everything is **backed up** before meddling with your software packages.

Ok, so you ran the other commands, everything is now up to date. The process was taking quite some time... but finally it's done, and you can now remove the obsolete packages and programs using this command:

```bash
sudo apt-get autoremove
```

When everything your system doesn't need anymore is removed, there can still be some leftovers (like obsolete dependencies or old config files).

You can try to delete these using:

```bash
sudo apt-get autoclean
```

### To recap...

Basically, your Ubuntu has several commands that you can run to get your system updated and cleaned up afterwards. To force upgrading and suppress those annoying `y/n` questions, you can add a `-y` modifier to the end of each command. You can also join commands by using the `&&` operator, which would make the whole "update + cleanup" sequence look like this:

```bash
sudo apt-get update && \
sudo apt-get upgrade -y && \
sudo apt-get dist-upgrade -y && \
sudo apt-get autoremove -y && \
sudo apt-get autoclean -y
```

You can eventually put this in a bash script and then configure the script to be runnable from the Terminal. You can do a quick search on the site here to see how to run scripts.

Just note what each of the commands does... for example, you probably don't want to `dist-upgrade` on each run of this snippet.
