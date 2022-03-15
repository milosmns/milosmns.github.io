---
layout: post
title: Android · Effortless Dialog Management
description: Reducing boilerplate code for dialog management on Android
date: 2018-06-02 15:00:00 +0100
image: '/images/posts/dialog.jpg'
tags: [dev, software, apps, android]
featured: false
---

**Boilerplate**. The magic word that opens any door in the Android world...

Let’s talk about showing Android dialogs, how to reduce the boilerplate and minimize maintenance code around managing dialogs. To support my desire to simplify dialog-related things, I worked a bit on something called `DialogManager`. Here’s what it does and how it works.

### Inspiration

To show a system dialog on Android (or an `appcompat` one), developers need to create a dialog builder first, then configure it for their specific needs, then create a new dialog instance out of it, and finally call the `show()` method on the dialog instance to present it to the user. It's not really tied to any kind of Activity or Fragment in any explicit and controllable way.

If the activity the dialog “lives” in is configured to allow configuration changes (such as rotation), you might be getting into the risky situation of having to deal with state saving and restoring of dialogs. You might also need to worry about avoiding memory leaks, e.g. managing the reference to the host Activity inside of a dialog that somehow "survives" the rotation. You'd also be managing the dismissal of the dialog and possibly showing it again after rotation has finished. You might also want to persist the initial configuration that the dialog had at creation time in order to re-create it identically to the first time it was created.

It's a lot of stuff to think about, and can become really annoying -- especially when you have multiple dialogs shown from the same page. Some would even say that the whole Dialog API is a bit... [silly](https://github.com/milosmns/silly-android). Well, the `DialogManager` I worked on aims to solve these issues and relieve you of having to write the boilerplate code yourself.

### The implementation

There are a couple of things to note about the flow when using this dialog manager. `DialogManager` is a simple, robust dialog management API designed around the (somewhat unfortunate) default flow of showing and hiding dialogs and dialog fragment on Android. It allows the user to show, hide, dismiss, and persist dialogs by using a combination of static dialog IDs and configuration Bundles, in a way that doesn't affect the surrounding code, and also helps keep the code very easy to maintenan.

##### Usage rules

  1. You are responsible for creating dialog instances by implementing the `DialogManagerCallback` interface. `DialogManager` will take care of showing the dialogs. The main entry point for you is the `DialogManager::show()` method. You have to be prepared that `DialogManager` can use your callback at any time after calling `show()` for the first time (due to configuration changes)
  1. All dialog instances (and their visibility) are managed by the `DialogManager` internally. Never keep any dialog instances in your Activities or Fragments, and always interact with the dialogs through the `DialogManager`
  1. You are responsible for choosing the static, unique IDs for each dialog you manage through the `DialogManager`. Simple constants should be good enough here
  1. All configuration options for the dialogs (dialog data, style, etc) should be sent through using a Bundle with the `DialogManager::show()` call. This Bundle will be persisted by the `DialogManager` for subsequent creation steps if needed, and it also gets passed as a method argument to the `DialogManagerCallback` that you implement
  1. On configuration changes such as rotation, you should use the save/restore methods using `Parcelable` data, they're on the `DialogManager` directly. These are used to persist the manager's state within the Activity or Fragment

### Sources

The `DialogManager` implementation is available as a part of the [SillyAndroid library](https://github.com/milosmns/silly-android) I've been working on lately. You can also go directly to the [DialogManager's Wiki page](https://github.com/milosmns/silly-android/wiki/DialogManager-Wiki) to find out more about it.

Happy dialog management! 😬
