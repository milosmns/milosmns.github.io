---
layout: post
title: Ubuntu · Running Shell files (.sh)
description: An opinionated guide
date: 2015-07-28 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

Open the Terminal. Make sure you know your file’s name and its location.Let’s say the name is `filename.sh` and it’s in the current directory you’re looking at. 

Remember, you can change the directory using the `cd` command. `cd myfolder` would get you into the `myfolder` directory.  
You can check your current directory using the `pwd` command, and list all files inside it using the `ls` command.

Your Shell file might still be a non-executable file. Either way, it's safe to make it executable again:

```bash
chmod +x filename.sh
```

... or if you need admin privileges to do so, then just add `sudo` in front, like this:

```bash
sudo chmod +x filename.sh
```

Now your file has the ability to be launched from the folder or from the Terminal. If you want to launch it from the Terminal, type in the following command:

```bash
sh filename.sh
```

... or using the current folder prefix (dot & slash):

```bash
./filename.sh
```

Again, if you need administrator privileges for the operation or something fails, you can just add the `sudo` prefix in front.
