---
layout: post
title: Ubuntu · Running Runnable files (.run)
description: An opinionated guide
date: 2015-07-31 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

Running and executing `.run` files is essentially the same as running `.sh` files.  
Start up your Terminal.

To allow the system to run the .run file, go into the directory where the file is located, then run this:

```bash
chmod +x file-name.run
```

Now that file is executable. To execute it, run:

```bash
./file-name.run
```

Since your .run file is probably a pre-built program, you should try running it first without admin privileges (without the `sudo` prefix command), and only then (in case of failure) run it with `sudo` again.

### More tips

I encountered some failures when executing .run files, like interface not opening up or my Terminal freezing. If you encounter these, you can try to stop your system's `x-server` service with this command:

```bash
sudo /etc/init.d/gdm stop
```

... or, if you have a newer system (like 12.04 LTS or later) you can try this command:

```bash
service gdm stop
```
