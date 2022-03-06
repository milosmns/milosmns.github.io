---
layout: post
title: Java Fun Facts · Performance (Part 4 of 4)
description: Performance and optimizations in Java, a multi-part series
date: 2015-09-18 15:00:00 +0100
image: '/images/posts/java.jpg'
tags: [dev, software, jvm]
featured: false
---

In this (final) part of the series, I'm looking into how fast comparing is for objects' classes. The source is again too long to include directly in this post, but [here's a link to it](https://github.com/milosmns/java-tests/blob/master/src/comparison/ClassComparisonTest.java) to check out.

### Investigation

Similarly to the last experiment, let's start with 2 classes:

  - `LevelOneClass` -- a POJO extending the `Object` class, implementing the `Cloneable` interface, and
  - `LevelTwoClass` -- an extension of the `LevelOneClass`
  
I'm having a bunch of instances of these two classes stored as Objects, shuffled inside a single huge collection. For comparison to that, I'll have another collection of the same objects, just shuffled differently.

By looping through the two collections, we can check know how quickly can the JVM compare classes of the belonging objects. (so, classes, not instances)

I could think of 5 different methods for comparison, some valid and some serving as a baseline:

  - Basic **reference comparison** check -- Using the operator `==`
  - Basic **equality** check -- Using the `equals()` method
  - Class **name** check -- Using the qualified `getName()` method from the object's `Class` and comparing these Strings
  - **Instance Of** check -- Using the `instanceof` operator
  - **Assignable From** check -- Using the `Class::assignableFrom()` method from the object's `Class`

### Results

The post would be too long to include the actual results directly, so here are the actual numbers [from the first test](https://gist.github.com/anonymous/1064b5e1c516a3c0a491), and [results from the second test](https://gist.github.com/anonymous/4843d046026bde7c325d).

##### Analysis

I did two tests on the same machine, using 500000 items in each of the lists, and ran every test 3 times to be sure. Since the JVM's power is affected by many things in your machine, you can’t really get a consistent set of results unless you run your experiments multiple times. But I do see a pattern.

**Reference comparison** was (in most cases) very fast, as expected. There were cases where it was super-slow (?!), but I guess these results were affected by some other stuff on my machine.

**Equality check** was also super-fast, which was a surprise to me. I expected it to be slower... but hey, we learn something new every day.

**Instance of** and **Assignable from** were both somewhere in the middle by looking at the speed stats. When split apart, they seems to be almost 2 times faster than the other methods. But there’s a catch, of course -- using them didn’t really compare the classes, it just uncovered inheritance patterns. But either way, I found out that both of these are **blazing fast**, faster than any other operation involving classes and class instances.

**Class name** was, as expected, the slowest of them all. It's literally comparing Strings, character by character. I did get an accurate result with this comparison though.

You learn something new every day. 😬
