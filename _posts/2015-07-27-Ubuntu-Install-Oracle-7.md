---
layout: post
title: Ubuntu · Installing Oracle's Java 7
description: An overview
date: 2015-07-27 15:00:00 +0100
image: '/images/posts/ubuntu.jpg'
tags: [linux, ubuntu, terminal, how-to]
featured: false
---

_Note: This was tested on 12.04, but should work for later versions as well._

#### Add the repository so that you have somewhere to pull JDK 7 from

```console
sudo add-apt-repository ppa:webupd8team/java
```

#### Update your machine's information about available software

```console
sudo apt-get update
```

#### Finally install Java

```console
sudo apt-get install oracle-java7-installer
```

Of course, if you need **Java 6**, **Java 8**, etc, just change the number in that last command. You can restart your machine if you want, but usually it's not necessary.

To test if it’s working, run this command:

```console
java -version
```

To see if compiling would work, run:

```console
javac -version
```
