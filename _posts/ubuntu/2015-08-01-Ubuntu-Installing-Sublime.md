---
layout: post
title: Ubuntu · Installing Sublime Test
description: An opinionated guide
date: 2015-08-01 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

If you're just starting with Ubuntu or Linux, you're probably having issues with installing new software. And that’s normal. And it's somewhat painful to do in the Terminal for first-timers.

Fortunately, Sublime Text 2 is available in a repository from the web update team ([webupd8team](http://www.webupd8.org/)), which makes installation much much easier. To add that repository to your local software sources list, run this command from the Terminal:

```bash
sudo add-apt-repository ppa:webupd8team/sublime-text-2
```

Now you have to update your available software list by running the following command:

```bash
sudo apt-get update
```

Now you have access to Sublime Text in its repository, and you can install it like so:

```bash
sudo apt-get install sublime-text
```

You can run Sublime Text from the Ubuntu menu (just type “Sublime” in the **Lens** menu). You can also run it from the Terminal using the `sublime-text` command, which then requires the file name after its call. 

So, an example of that:

```bash
sublime-text myfile.txt
```

or, if you need admin privileges:

```bash
sudo sublime-text myfile.txt
```

#### Later versions

You might be interested in Sublime Text 3 instead. You should be aware that ST3's command line tool has been renamed to `subl` (instead of `sublime-text`).
