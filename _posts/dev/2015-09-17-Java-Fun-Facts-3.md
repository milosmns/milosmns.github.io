---
layout: post
title: Java Fun Facts · Performance (Part 3 of 4)
description: Performance and optimizations in Java, a multi-part series
date: 2015-09-17 15:00:00 +0100
image: '/images/posts/java.jpg'
tags: [dev, software, jvm]
featured: false
---

### Idea phase

This experiment is a bit more complex than the previous two experiments in this series. It consists of looping through 2 different lists and comparing the objects inside them using different equality methods to see which of them work, which don’t, which ones are slow and which are fast. 

The basic pseudo-code would be:

```python
for j in size(lists) {
  compare listA[j] to listB[j]
}
```

The source on this test is quite complex, so I couldn't simply run it on IDE One like before. But hey, I'm still [sharing the sources](https://github.com/milosmns/java-tests/blob/master/src/comparison/InheritanceObjectsComparisonTest.java), so you can run this locally.

### Investigation

I am going to be testing 2 different scenarios - one uses class inheritance and the other one doesn't.

##### Setup

In the first example, our base class extends `java.lang.Object` (POJO) and implements the `Comparable` interface -- so nothing extraordinary and nothing fancy. In a dramatic twist, the other class extends that first class.

I decided to call them `LevelOneClass` and `LevelTwoClass`.  
`LevelOneClass` is basically bundling 2 Strings, while `LevelTwoClass` is an extended version of the previous class, adding one more String to the bundle.

##### Investigation

Now to the interesting part, the comparison. I came up with 5 comparison methods, some of them reliable and some serving as the baseline:

  - **Plain old equals**: Comparing using `equals()` on both objects
  - **Plain old hash-code**: Comparing using `hashCode()` on both objects
  - **Super's equality**: Instead of comparing the object content itself, this one calls `super.equals()` to check
  - **Super's hashing**: Analoguous to super's equality, this calls to `super.hashCode()` to check
  - **Reflection**: This one is big and tricky. The process is to fetch all fields in the class, make them accessible, and then compare those to the other class using the `equals()` method on each field. If a single field fails the comparison, the whole comparison returns `false`. This one should be the most precise version, as it deeply inspects the whole object's structure and its data (albeit probably the worst performer)

On to the fun part -- results. The test was quite extensive and long, so I can't share the full output directly in the post, but I can link to the results:

  - [500000 objects per list](http://pastebin.com/3SsMj8VJ)
  - [1 million objects per list](http://pastebin.com/kvwKdNPF)

### Results

It seems that the good-old manual comparison by `equals()` comes in first, even faster than the `hashCode()` variant. Of course, `super.equals()` is way faster, but it’s incorrect and serves only as the baseline.

As expected, our reflective comparison is the slowest.
