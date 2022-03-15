---
layout: post
title: Android · Blinker View
description: A small library with a View component that simply blinks
date: 2018-05-11 15:00:00 +0100
image: '/images/posts/traffic-light.jpg'
tags: [dev, software, apps, android]
featured: false
---

#### Inspiration

I finally found some time to do the stuff I like to do (write code). As a result of that, I built a simple blinking Android View as a standalone library, called [BlinkerView](https://github.com/milosmns/blinking-image-view). What it does is already in the name -- it basically infinitely blinks using the source image you give it.

The reason why I had to build this myself is that most of the solutions on "how to blink android view" all over the Internet suggest to use the **Animation** class and animate the View’s alpha from 0% to 100% through bouncing. The problem with this approach is that the background Drawable also gets affected by the alpha changes.

#### Details on the approach

If you have a static background on the blinking ImageView (let's say a ring or a bordered circle) and then you have a red dot on top of it (the source image of the ImageView), you're using 2 Drawables on a single View. If you then call something like `startBlinking()` which, for example, triggers the suggested alpha-changing Animation, both the ring (bordered circle) and the red dot in the middle will start blinking.

There is a workaround for this issue -- adding a static View behind, or maybe a `wrap-content` FrameLayout with a background ring as a container for the ImageView. When you start to blink the ImageView, it will appear as if the background of the ImageView is not blinking, but in fact it will be the background of the parent container that is not blinking (your ImageView has no background). It's not great... it's a hacky workaround.

I just didn’t want to place a dummy container whenever I want to blink an ImageView. 😬

So, with this library, the background never blinks -- only the given source image blinks. You can then put any kind of background on the View, and it will stay there statically, without any changes.

#### Source

You can find the sources:

  - [GitHub Repository](https://github.com/milosmns/blinking-image-view)
  
Have fun blinking!
