---
layout: post
title: Java Fun Facts · Performance (Part 2 of 4)
description: Performance and optimizations in Java, a multi-part series
date: 2015-09-16 15:00:00 +0100
image: '/images/posts/java.jpg'
tags: [dev, software, jvm]
featured: false
---

After some interesting findings in the first part of this series, I am now interested in testing `while` loops in a standard JVM.

#### Investigation

Here's the code:

```java
class Looping {

  private static class Log {

    public static void logLoopStats(
      String name, 
      long elapsedNano, 
      int charCount
    ) {
      float timePerChar = (float) elapsedNano / (float) charCount;
      String part1 = String.format(
        "%s: %,dns, character count: %,d. ", 
        name, 
        elapsedNano, 
        charCount
      );
      String part2 = String.format(
        "Time per character is %.3fns.", 
        timePerChar
      );
      System.out.println(part1 + part2);
    }

  }

  public static void main(String[] args) throws Exception {
    List<String> list = new ArrayList<>();

    for (int j = 0; j < 1000000; j++) {
      list.add("one");
      list.add("two");
      list.add("three");
      list.add("four");
      list.add("five");
    }

    long startTime1 = System.nanoTime();
    int count1 = loopWithI(list);
    long elapsed1 = System.nanoTime() - startTime1;

    long startTime2 = System.nanoTime();
    int count2 = loopWithISize(list);
    long elapsed2 = System.nanoTime() - startTime2;

    long startTime3 = System.nanoTime();
    int count3 = loopWithIterator(list);
    long elapsed3 = System.nanoTime() - startTime3;

    long startTime4 = System.nanoTime();
    int count4 = loopWithListIterator(list);
    long elapsed4 = System.nanoTime() - startTime4;

    Log.logLoopStats("Loop with I, counting size", elapsed1, count1);
    Log.logLoopStats("Loop with I, cached size", elapsed2, count2);
    Log.logLoopStats("Loop with iterator", elapsed3, count3);
    Log.logLoopStats("Loop with list iterator", elapsed4, count4);
  }

  private static int loopWithI(List<String> list) {
    int i = 0;
    int charCount = 0;
    while (i < list.size()) {
      charCount += list.get(i).length();
      i++;
    }
    return charCount;
  }

  private static int loopWithISize(List<String> list) {
    int i = 0;
    int charCount = 0;
    int size = list.size();
    while (i < size) {
      charCount += list.get(i).length();
      i++;
    }
    return charCount;
  }

  private static int loopWithIterator(List<String> list) {
    Iterator<String> iterator = list.iterator();
    int charCount = 0;
    while (iterator.hasNext()) {
      charCount += iterator.next().length();
    }
    return charCount;
  }

  private static int loopWithListIterator(List<String> list) {
    ListIterator<String> listIterator = list.listIterator();
    int charCount = 0;
    while (listIterator.hasNext()) {
      charCount += listIterator.next().length();
    }
    return charCount;
  }

}
```

[Here is](https://github.com/milosmns/java-tests/blob/master/src/loops/whilel/WhileLoopTest.java) the original source, and you can run it on [IDE One](http://ideone.com/Td0jy8) yourself.

#### Results

The results for 5 different Strings, repeated 1M times:

```console
Loop with I, counting size: 95,307,356ns, character count: 19,000,000. Time per character is 5.016ns.

Loop with I, cached size: 59,286,751ns, character count: 19,000,000. Time per character is 3.120ns.

Loop with iterator: 86,909,725ns, character count: 19,000,000. Time per character is 4.574ns.

Loop with list iterator: 85,995,007ns, character count: 19,000,000. Time per character is 4.526ns.
```

It seems like we have the same result as before with `for` loops. The regular `while` loop with a predefined iteration length is much faster - approx. **40% faster** than other loops.

The strange thing here was that the good-old `while-i` loop was the slowest one! Even the iterators performed better... not sure what to think.
