---
layout: post
title: Android · Multi-Window Support
description: Looking into how Android is picking the correct resource when rendering multi-window layouts
date: 2017-11-17 15:00:00 +0100
image: '/images/posts/window-split.jpg'
tags: [dev, software, apps, android]
featured: false
---

#### Inspiration

If you’re supporting Android Nougat (OS 7.0-7.1, SDK 24-25), you probably know that one of the biggest changes introduced is the support for [multi-window user experience](https://developer.android.com/guide/topics/ui/multi-window.html). Most of the apps are now allowing users to get into the new, minimized viewing mode. But, you’re probably also [having issues](https://stackoverflow.com/questions/tagged/android-7.0-nougat%20multi-window%20android?mode=all) while preparing apps for the split-screen view... I sure am... so, I wanted to create a demo app to share an example of how Android chooses which layout to render.

#### Structure

My idea is to create an app that would display the current configuration on the screen. It will show the following information:

  1. Activity orientation
  1. Device orientation
  1. Activity mode (full-screen vs. split-screen)
  1. Mode change origin (what triggered the configuration change)

Stock Android Nougat offers 3 split-screen configurations while in portrait mode: `1:2`, `1:1`, and `2:1`. While in landscape mode, there is only one split-screen configuration: `1:1`.

{:refdef: style="text-align: center;"}
![Portrait 1-1](/images/posts/split-port-1-1.png)
*Portrait mode / 1:1*
{: refdef}

{:refdef: style="text-align: center;"}
![Portrait 2-1](/images/posts/split-port-2-1.png)
*Portrait mode / 2:1*
{: refdef}

{:refdef: style="text-align: center;"}
![Portrait 1-2](/images/posts/split-port-1-2.png)
*Portrait mode / 1:2*
{: refdef}

{:refdef: style="text-align: center;"}
![Landscape 1-1](/images/posts/split-land-1-1.png)
*Landscape mode / 1:1*
{: refdef}

**Note** -- Samsung devices offer finer control over the split ratio, which I personally find completely useless, and that behavior introduces some issues with detecting the configuration, of course... more on Samsung a bit later.

#### Under the hood

This app will detect the current activity's split-screen configuration. By looking at the app, we’ll know which layout was be loaded by the OS. Moving between stock Android's split-screen configurations will always trigger an Activity’s recreation cycle: `pause` → `stop` → `destroy` → `create` → `start` → `resume`. So, yes, the **full cycle**. 

I'll also be using a library I’ve been working on ([SillyAndroid](https://github.com/milosmns/silly-android#silly-android)). If you check out the source code, you’ll see that there is nothing special about these checks and you can do them manually if you prefer to. It's just resources in resource folders and switch/case/when clauses in bytecode.

To be able to see which mode and configuration our Activity is currently in, we’ll need an empty layout with a TextView in the center of the Activity. This View is going to be updated each time something triggers a mode change.

###### The fun part

We need to find the current Activity’s orientation, but also find the whole device’s orientation (assuming there is only one screen).

```kotlin
val orientations = ... // magic, trust me, see the source later
val activityOrientation = orientations(this)
val deviceOrientation = orientations(applicationContext)
```

The trick here is to use the **Application** Context to detect the current screen’s orientation, and use the **Activity** Context to detect the current Activity’s orientation. This comes in handy especially when in split-screen mode.

Let's use the backward compatible check for multi-window and convert the result into a String for displaying it cleanly.

```kotlin
val isMultiWindowMode = SillyAndroid.UI.isInMultiWindowMode(this)
val screenMode = if (isMultiWindowMode)
  "split-screen" else "full-screen"
```

When you have this data ready, just populate the TextView:

```kotlin
textView.text = "Activity is now in $screenMode mode,\n" +
  "$activityOrientation.\n" +
  "Device is in $deviceOrientation.\n"
```

To be sure that the description was really changed, we’ll also recolor the visible views to some random colors. Both `Coloring` and `getContentView()` come also from my Silly Android library.

See the coloring code:

```kotlin
val backgroundColor = ... // magic, trust me, see the source later
getContentView<ViewGroup>().setBackgroundColor(backgroundColor)
textView.setTextColor(Coloring.contrastColor(backgroundColor))
```

Now, if we put all of that into a single function, we can call the function from the Activity’s `onCreate()` callback, and check the results in the UI.

### Samsung...

As you may know by now, Samsung always has their own way of doing things... and split-screen is not an exception. Apart from offering all of the mentioned ratios by default, they also offer a slider to make the apps split anywhere across the screen. It seems useful, right? It's not, and it's not worth the headache that comes with such a feature.

The feature, of course, causes new issues. Dragging and releasing the slider **anywhere else but** on `1:1`, `1:2` or `2:1` ratios **will not cause the activity to be recreated**.

How can we detect any changes, given that the Activity is not recreated?

Well, there's a workaround. You need to track the Configuration changes manually. There is no need to add anything in the `AndroidManifest` for this tracking, just override the `onConfigurationChanged()` callback on the Activity. To detect if split-screen ratio and window size has changed, you need to look for a `screenSize` changed flag. This also means that you need to save the last configuration somehow...

The code snippet is below.

```kotlin
override fun onConfigurationChanged(config: Configuration?) {
  super.onConfigurationChanged(config)
  config?.let {
    val interestingFlag = ActivityInfo.CONFIG_SCREEN_SIZE
    if (it.diff(savedOldConfig) and interestingFlag != 0) {
      savedOldConfig = Configuration(config)
      updateDescription()
    }
  }
}
```

### Closing words

After analyzing the results from the demo app, I found the following.

##### Activity is in the smaller window, ratio 1:2

  * Activity orientation is `landscape`
  * Screen/device orientation is `portrait`

##### Activity is in the half-screen window, portrait, ratio 1:1

  * Activity orientation is `landscape` (**!**)
  * Screen/device orientation is `portrait`

##### Activity is in the bigger window, ratio 2:1

  * Activity orientation is `portrait`
  * Screen/device orientation is `portrait`

##### Activity is in the half-screen window, landscape, ratio 1:1

  * Activity orientation is `portrait` (**!**)
  * Screen/device orientation is `landscape`

### Sources

You can find the app's source:

  - [GitHub Repository](https://github.com/milosmns/split-screen-test)

To download the app and test for yourself:

  - [GitHub Releases](https://github.com/milosmns/split-screen-test/releases/tag/v1.2)

Have fun split-screening! 😬
