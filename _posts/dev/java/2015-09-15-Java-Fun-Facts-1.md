---
layout: post
title: Java Fun Facts · Performance (Part 1 of 4)
description: Performance and optimizations in Java, a multi-part series
date: 2015-09-15 15:00:00 +0100
image: '/images/posts/java.jpg'
tags: [dev, software, jvm]
featured: false
---

#### Investigation

Do you know how quick or slow different `for` loops are on a standard Java Virtual Machine?

Take a look at this example and the different looping approaches:

```java
public class Main {

  private static int loop1(List<String> list) {
    int charCount = 0;
    for (int i = 0; i < list.size(); i++) {
      charCount += list.get(i).length();
    }
    return charCount;
  }

  private static int loop2(List<String> list) {
    int charCount = 0;
    int listCount = list.size();
    for (int i = 0; i < listCount; i++) {
      charCount += list.get(i).length();
    }
    return charCount;
  }

  private static int loop3(List<String> list) {
    int charCount = 0;
    for (String s : list) {
      charCount += s.length();
    }
    return charCount;
  }

  public static void main(String[] args) {
    List<String> ls = new ArrayList<String>();

    for (int j = 0; j < 1000000; j++) {
      ls.add("one");
      ls.add("two");
      ls.add("three");
      ls.add("four");
      ls.add("five");
    }

    long startTime1 = System.nanoTime();
    int count1 = loop1(ls);
    long elapsed1 = System.nanoTime() - startTime1;

    long startTime2 = System.nanoTime();
    int count2 = loop2(ls);
    long elapsed2 = System.nanoTime() - startTime2;

    long startTime3 = System.nanoTime();
    int count3 = loop3(ls);
    long elapsed3 = System.nanoTime() - startTime3;

    System.out.println("Elapsed1: " + elapsed1 + " ns");
    System.out.println("Elapsed2: " + elapsed2 + " ns");
    System.out.println("Elapsed3: " + elapsed3 + " ns");
  }

}
```

**Loop 1** is a regular `for-i` loop using the index and checking the list length each pass.

**Loop 2** is a regular `for-i` loop using the index but **not checking** the list length each pass.

**Loop 3** is an `enhanced for loop`, internally using iterators.

The original sources are [here](https://github.com/milosmns/java-tests/blob/master/src/loops/forl/ForLoopTest.java), and you can run the code on [IDE One](https://ideone.com/2rmQDp).

#### Results

The results from 10 different Strings, repeated 1 million times:

```console
Elapsed1: 183943668 ns
Elapsed2: 107588701 ns
Elapsed3: 167478689 ns
```

More results, 5 different Strings, repeated 1 million times:

```console
Elapsed1: 99760529 ns
Elapsed2: 59375177 ns
Elapsed3: 90220306 ns
```

These indicate that the `for-i` loop without the list size check (loop number) is the fastest one by far, approximately **40% quicker** than others from this example.

I found this quite surprising, given that in each case the list was an `ArrayList`. I'm going to do some more experiments on Java performance topics to see what else I can find.
