---
layout: post
title: Ubuntu · Setting up JAVA_HOME environment variable
description: An opinionated guide
date: 2015-08-22 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

_Note: This works for Oracle's Java installed through an external repository (you can the find instructions here on the site). Do your own search for other installations._

### Installation for Bash

First you need to edit your Unix user's config file that contains your environment variables and your access path. My editor is Sublime Text (find installation on the site here). Any other editor that supports command line is fine as well (like GEdit, nano, vim, etc).

By default, your Ubuntu comes with `bash`. Open a file called `.bashrc` in your Home directory:

```bash
sudo sublime-text ~/.bashrc
```

Then, add the following lines to the end of your config file:

```bash
JAVA_HOME=/usr/lib/jvm/java-7-oracle
export JAVA_HOME
```

Shorter version is:

```bash
export JAVA_HOME=/usr/lib/jvm/java-7-oracle
```

but this doesn't work on all versions of Bash. When done editing, save the file and re-source the config files:

```bash
source ~/.bashrc
```

or shorter: 

```bash
. ~/.bashrc
```

Optionally (almost never necessary), you can restart the machine:

```
sudo reboot now
```

#### Z-Shell

In case you're using `zsh` instead of `bash`, your config file will be `~/.zshrc` instead -- but since you have z-shell you probably already know that.
