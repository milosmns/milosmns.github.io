---
layout: post
title: Android · Tasks and Back Stack
description: A deeper look into Android's handling of fragments, activities and its internal backstack and task managers used in navigation
date: 2017-01-25 15:00:00 +0100
image: '/images/posts/tea-cup-stack.jpg'
tags: [dev, software, apps, android]
featured: false
---

### Inspiration

If you ever created an app that has more than 2 activities, it’s likely that you needed to change the [launch mode](https://developer.android.com/guide/topics/manifest/activity-element.html#lmode) for some of them. I must admit that the whole thing is still a bit confusing to me...  Normally, I need to visualize everything in order to fully understand what happens -- that's what I was going to do with the screen navigation back stack too. There was a lot of information online already (also a lot of useless stuff, heh) but eventually I decided to create a simple app to demonstrate how activity stacking actually works and what happens inside.

### Experiment setup

The app binary can be [found here](https://github.com/milosmns/android-task-stack-example/releases/tag/v1.2), and the source [is here](https://github.com/milosmns/android-task-stack-example). I wrote it in Kotlin, but you’ll get the idea of how things work even if you don’t have any experience with Kotlin.

On to the main point.

The app shows the activity title on top of each screen, describing what kind of activity you’re currently looking at. It also displays that activity’s Intent origin (where it was started from). Next to it, each screen also shows the current activity’s task ID, and the corresponding task ID from the origin activity.

Below all of that, there’s a list of currently active tasks from the OS -- or, at least the tasks we could access using the new API) -- so that you can see exactly what happens when you switch to another activity. You should only be interested in the launcher task and your app’s tasks and ignore the other ones.

To change/switch/go to another type of activity, just use one of the buttons at the bottom, options are: `default`, `singleTop`, `singleTask`, `singleInstance`. You can read more about the tasks and back stack from the [official docs](https://developer.android.com/guide/components/activities/tasks-and-back-stack.html), or take a look at this [explanation video](https://www.youtube.com/watch?v=MvIlVsXxXmY) presented by Google's team.

### Results

To illustrate what I detected during this task and backstack experiment, I created a video using the app mentioned above and going through various scenarios, recording all of that and then wasting a few hours on preparing the output. **Warning**: there's some irritating background music I couldn't get rid of. 😬

<p><iframe
  src="https://player.vimeo.com/video/201011854"
  title="Experiment results"
  width="640"
  height="360"
  frameborder="0"
  allowfullscreen
></iframe></p>
