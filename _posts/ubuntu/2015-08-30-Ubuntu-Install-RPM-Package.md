---
layout: post
title: Ubuntu · Installing RPM packages
description: An opinionated guide
date: 2015-08-30 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

So you have an `.rpm` package downloaded but have no clue how to convert it to `.deb` format and install on your Ubuntu? No worries, there's a quick and simple solution to that problem.

First you need to install a few software packages that help you convert `.rpm` to `.deb`. Those are: `alien`, `dpkg-dev`, `debhelper`, `build-essential`.

Open your Terminal and type:

```bash
sudo apt-get update
```

That step helps pull in the latest required software repositories. Check on this site on more about software updates in Ubuntu.

Installation of the required packages:

```bash
sudo apt-get install alien dpkg-dev debhelper build-essential
```

Now you can do the conversion. From the same Terminal window, go to your `Downloads` directory (or wherever you downloaded the RPM package to). Execute like this:

```bash
sudo alien YOUR_INSTALLATION_NAME.rpm
```

When that’s done, you'll have a `.deb` file with the same name. You can either double-click the newly created installation file from the file browser or simply install it from the Terminal:

```bash
sudo dpkg -i YOUR_INSTALLATION_name.deb
```
