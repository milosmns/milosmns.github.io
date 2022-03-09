---
layout: post
title: Silly Android
description: A utility library for Android that helps with automating the same, repetitive, day-to-day tasks when building Android apps
date: 2017-06-10 15:00:00 +0100
image: '/images/posts/repair-man.jpg'
tags: [dev, software, apps, android]
featured: false
---

### The initial release

If you met me in recent months, you've heard my complaining about the same Android chores over and over. Well, the work on that is done, the chores are now automated, and my utility library **Silly Android** is ready for a release.

I'm hopeful that this work primarily addresses the most common issues with the Android APIs nowadays, while also allowing us to quickly start up new projects and maintain the older ones more easily.

Why "Silly", you may ask? Because the original API decisions are just silly, so I decided to call the fixes that way too.

Contributions are welcome:

  - [GitHub repository](https://github.com/milosmns/silly-android)

### Updates and future releases

An update as per **mori-honest**'s request ([see here](https://github.com/milosmns/silly-android/issues/4)), Silly Android now also includes access to the software keyboard. Read more below.

To detect when soft keyboard is shown:

```java
@Override
public void onKeyboardShown(int size) {
  Log.d(TAG, "Current keyboard size is: " + size);
}
```

To detect when soft keyboard is hidden:

```java
@Override
public void onKeyboardHidden() {
  Log.d(TAG, "Current keyboard is hidden!");
}
```

To hide the keyboard on command, e.g. after a click event:

```java
hideKeyboard(); 
```

All of these are directly available in Silly Android’s `Easy` components, i.e. `EasyActivity`, `EasyFragment`, `EasyDialog`, and transitively available in all `Parsable` components.

#### The future

I hope that with Kotlin we won't need utilities such as Silly Android anymore.  
But until then, this fixes a lot of the _silly_ APIs. 😬
