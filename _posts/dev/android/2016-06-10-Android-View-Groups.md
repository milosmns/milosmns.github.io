---
layout: post
title: Android · Visibility handling in ViewGroup
description: Android strikes back! How are ViewGroups handling visibility for their child Views? Do you know? I didn't!
date: 2016-06-10 15:00:00 +0100
image: '/images/posts/hiding.jpg'
tags: [dev, software, apps, android]
featured: false
---

Disclaimer: if you’re new to Android, you’ll most likely have to go through some basics first to understand the catch presented here. If you have some experience already, here’s an interesting question for you:

> Does changing visibility on a ViewGroup set the same visibility to all of its children?

The short answer: at the time of writing this post, **no**.

### The long answer

Let's imagine that you have a View container, e.g. a `LinearLayout`, `RelativeLayout`, `FrameLayout`. And now you have a View inside, doesn’t matter which one. You want to hide the container from the screen. That’s easy, right? Just call `setVisibility(GONE)` on it and you’re done.

Now imagine you have a custom-built View that reacts to visibility changes. In this custom View, you simply override the `setVisibility()` method and you’re done. Now you're able to react to visibility changes, and do whatever you need to do at that point (for example: stop an animation).

Next, your custom view is inside the View container from above. Setting visibility on the container **will not** trigger a visibility change on its children -- therefore your animation would still keep running. The final effect on the UI may be the same -- the container and its child Views are not visible to the user anymore -- but technically speaking, you didn’t make any changes to the child views (and therefore didn’t react properly).

This happens both from Java and XML.

#### Less talk, more examples!

To illustrate the behavior, I made a [demo app](https://github.com/milosmns/demo-child-view-visibility), go check that out. You can also directly [download the APK](https://github.com/milosmns/demo-child-view-visibility/blob/master/resources/Visibility-Demo.apk?raw=true) too if you wish.

People have already asked about this behavior [here](http://stackoverflow.com/questions/19775407/effect-of-setting-parent-view-visiblity-on-its-children), and there are some explanations offered, so the link may be worth checking out.

To go deeper, you can check out the [LayoutInflater's source](https://github.com/android/platform_frameworks_base/blob/master/core/java/android/view/LayoutInflater.java#L796) and follow the recursive child inflation sequence. You can then check out the interesting [“_snapshot_” method on the ViewGroup class](https://github.com/android/platform_frameworks_base/blob/master/core/java/android/view/ViewGroup.java#L3160), or take a look at the original [visibility implementation on the View class](https://github.com/android/platform_frameworks_base/blob/master/core/java/android/view/View.java#L7430). All of this confirms my earlier statement.

The problem is especially problematic if you're stopping animations on `setVisibility(GONE)`, because animations tend to reset visibility to `VISIBLE` on animation loop restart.

#### Conclusions

To conclude, **this behavior is intentional**. You can easily work around it only by overriding the ViewGroup class' behavior, and then setting the visibility to children manually for your custom View containers.

Watch out for the performance hit this introduces during the measure/layout sequence though.
