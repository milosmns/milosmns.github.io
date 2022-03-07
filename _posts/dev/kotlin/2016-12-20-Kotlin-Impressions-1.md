---
layout: post
title: Learning Kotlin! Adventure, part 1 of 2
description: Playing around and getting to know Kotlin, a relatively new programming language for the JVM and Android
date: 2016-12-20 15:00:00 +0100
image: '/images/posts/kotlin-island.jpg'
tags: [dev, software, apps, android, kotlin]
featured: false
---

### Where I'm coming from

If you’re an Android developer today, you’re probably doing something like this:

  1. Create a layout for an Activity in your `activity.xml`
  1. Create a Java file for your activity, like `MyActivity.java`
  1. Declare the activity in your `AndroidManifest.xml`

Right? But there's more -- inside of your `MyActivity` class, you’d do more work:

  1. Add a lot of boilerplate around `findViewById()` to map your Views from `activity.xml`'s layout to the class' fields
  1. Add a lot of code to assign, reassign and remove various listeners
  1. Add a lot of code to structure your events and app architecture
  1. Add a lot of utility methods and classes that help you accomplish various seemingly simple tasks -- tasks that usually require code duplication because of how Android APIs are built
  1. Pull in a lot of libraries with Gradle to ease your development process for Android apps
  1. Pull in a lot of libraries with Gradle to help you reduce the amount of Java code needed to accomplish other (again, seemingly simple) tasks

Again, right? You feel my pain?

It's quite repetitive. The whole process is unpleasant even for experienced Android developers. What's maybe even worse, the process is very similar to almost all platforms based on the Java language on JVM.

### Welcome, Kotlin

[Kotlin](https://kotlinlang.org) -- a relatively new, statically-typed language developed for the [JVM](https://en.wikipedia.org/wiki/Java_virtual_machine) by [JetBrains](https://www.jetbrains.com) -- has set out to improve all of the situations mentioned above, and as far as I can see... it’s doing a pretty good job at that!

This multi-part post contains my thoughts on the matter, some real-world examples, and of course a simple demo you can test and analyze with the source code provided.

### The first steps

My journey with Kotlin started several months ago when I read a blog post about using Kotlin in a production environment for a client, and the writer was surprised when his customer was OK with him using Kotlin. Naturally, I was interested in finding out what Kotlin is exactly in the first place, but also why using it would be a problem for clients.

The first thing I found out was that Kotlin is “just another language”, and I was immediately annoyed by the fact that people are still trying to develop new languages in spite of the enormous, (almost) political influence of huge companies like Oracle, Google, Microsoft and Apple. Like, why? Do we need it? My opinion at the time was that inventing a new JVM language in this day and age was a complete waste of time, so I just left the website and didn’t come back for a while. Another thing that discouraged me was that Kotlin was not at version `1.0` yet, which is something I see immediately as a potential issue with clients...

A few months later, I was reading another blog post about an issue I was having with Doze mode on Android, and the writer explained the issue in detail with really good code examples -- but guess what language he used? Yup, it was Kotlin. I looked through the other examples, and I found that there was “something wrong” with the code I was looking at.

The source contained something like this:

```kotlin
val people = getPeople() // this returns a ‘People’ object
val women = people.getWomen() // this also returns a ‘People’ object
val men = people - women // ‘men’ is also a ‘People’-type object
println(Calculation(men)) // no ‘new’ keyword?
```

**Wait, what?**

That's not JavaScript, phew! Okay, so... there's something bothering me. Am I reading this right? Subtracting an `Object` from another `Object`? Coming from a Java world (and not C#), this was very weird to see. My previous experience with PHP, JavaScript, Shell, ActionScript, etc. showed me a lot of strange stuff -- but this was out of the ordinary for a JVM language. I quickly found out that Groovy does something similar with its DSL extensions, but Kotlin’s syntax was the first time I saw [operator overloading](https://kotlinlang.org/docs/reference/operator-overloading.html), for example. This is no plugin, this is the real deal. It’s built in, the functionality comes bundled inside the Kotlin compiler. Interesting, right? Btw, did you know that you can [try Kotlin live](https://try.kotlinlang.org) on their website? I sure didn’t.

The next thing I noticed was the shortened syntax in comparison to Java. Sure, it uses the standard Pascal notation for parameters, Pascal-cased class names, camel-cased variable names, curly brackets to start/end blocks, etc. All of that was familiar, but it was somehow so short! What is normally 3-4 lines in Java, is like 1 line in Kotlin! Then I got more interested, so I discovered more of the Kotlin world, including `inline` functions, `infix` functions, `extension` functions, and `higher-order` function types.

Here's another example:

```kotlin
val list = mutableListOf(1, 2, 3) // where's this import coming from?
list.swap(0, 2) // how is this possible? where is swap() defined?
println(list) // output is [3, 2, 1]. toString() is automatic?
```

A few new things happening here. That `mutableListOf()` call is a call to Kotlin's `stdlib` package. No qualifier class? Nope, not needed. Functions and properties can be **first-class citizens** in Kotlin. This means that you can have functions defined **outside** of Kotlin classes. Just slap your function directly into the `.kt` file, like in Python.

Moving on -- the `swap()` function... here's the definition of that function:

```kotlin
// Swapping is an "extension" function
fun <T> MutableList<T>.swap(index1: Int, index2: Int) {
  val tmp = this[index1] // 'this' is a MutableList instance
  this[index1] = this[index2]
  this[index2] = tmp
}
```

Woah, nice! An [extension function](https://kotlinlang.org/docs/reference/extensions.html) allows you to introduce additional class functionality without actually inheriting from the class. Quite interesting, similar to something C# has.

Finally, how did the list output from that example "just work"? Well, Kotlin has [smart type-casting](https://kotlinlang.org/docs/reference/typecasts.html), so it knew how to convert the list Object into the desired String value. There's also stuff like `joinToString()` on all Collections where you can specify a delimiter and other interesting stuff around getting a custom-formatted String from a Collection.

### Into the rabbit hole

After using Kotlin for a while in some of my hobby projects, I was amazed at how lovely Kotlin was to work with. How can **you** try it? Well, just go to the official website and follow the step-by-step instructions, it’s super easy. I installed an IntelliJ IDEA plugin that allows me to automatically convert Java to Kotlin directly inside the IDE, so that’s an option too. It's coming to IntelliJ IDEA as a built-in plugin soon.

Anyway, I’ll try to quickly brush on some of the things most people are interested in. Weird or bad things first.

  * Small community for now
  * Supported in IntelliJ products only for now
  * Classes are `final` by default (or... this may be good?)
  * No implicit conversion between `int` and `long`
  * Not all 3rd-party libraries support Kotlin directly

I read that JetBrains is working hard on resolving all of these, so... stay tuned?

Now, on to the good stuff.

  * **Compilation speed using Gradle**. Recently introduced incremental compilation works well, so compiling is really fast now
  * **Kotlin IDEA plugin performance**. It's really fast and convenient
  * **Annotations**. No problems for me, either I’m not using the problematic annotations, or they made everything work out of the box
  * **Tests**. You can write tests in Kotlin, it’s super easy
  * **Interoperability with Java**. Believe it or not, you can use Kotlin code from Java, and Java code from Kotlin. This means that you can keep your production code written in Java and write tests in Kotlin. Or you can gradually migrate to Kotlin if you wish
  * **Compile output**. Kotlin can compile into JVM bytecode that works perfectly on standard and Android JVMs, or even into JavaScript to debug or run in the browser
  * **Functional programming**. Kotlin does not force you to learn functional programming, but it allows you to use higher-order functions and lambdas if you want to
  * **Java versions**. Kotlin targets Java 6 today, so no issue there either
  * **Documentation and tutorials**. JetBrains gave a great reference doc with examples of everything. Everything is open-source on GitHub, so you can check it out at any time
  * **Data classes**. _(personal favorite)_ A simplified way of generating `data` classes to avoid boring boilerplate code such as `hashCode()`, `equals()`, `copy()` and `toString()`. Also removes getters and setters and overloaded constructors
  * **Learning curve**. Depends on you, really. But it’s definitely something fun to try out!

Oh, right, I almost forgot! One more thing. 😬
Kotlin is completely [null-safe](https://kotlinlang.org/docs/reference/null-safety.html) **at compile-time**. Ready to switch?!

```kotlin
var a: String = "abc"
a = null // compilation error, ‘String’ is a non-null type

var b: String? = "abc"
b = null // this is ok, because ‘String?’ is a nullable type

val len = a.length // compiles fine, no way to cause an NPE
len = b.length // compilation error: variable 'b' can be null
len = b?.length // this is ok, ‘?.’ checks for nullability first
```

### Conclusion of part 1

These were just a few interesting examples of how Kotlin works, what it looks like, and what it offers (there’s **a lot more** on the [official website](http://kotlinlang.org)). If you prefer books, here's [a good read](https://www.manning.com/books/kotlin-in-action#downloads) by one of the authors of the Kotlin language.

In my future posts I’ll focus on real-world applications and the hobby project I have been working on using Kotlin.
