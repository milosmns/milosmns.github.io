---
layout: post
title: Android · Circular Slider
description: A free UI element for circular (round) number picking
date: 2015-12-15 14:00:00 +0100
image: '/images/posts/circle-slider.png'
tags: [dev, software, android, open-source]
featured: false
---

> What goes around, comes around!
>
> <cite>Justin Timberlake</cite>

Thanks, Justin! But seriously, that pretty much sums it up.

I published a Circular Slider for Android. It's a simple View, it goes around in a circle, and you can color it using your own custom colors.

The usage is straightforward:

```xml
<me.angrybyte.circularslider.CircularSlider
  app:angle="3.14"
  app:border_color="#505090"
  app:border_thickness="14dp"
  app:border_gradient_colors="#f05151;#4a90e2;#4a90e2"
  app:thumb_color="#30AEFF"
  app:thumb_size="24dp" />
```

Many thanks to [@bistabil](https://github.com/bistabil) for working on this one and credit to [@staacopy](https://dribbble.com/staacopy) for the graphics.

Here's the source:

  - [GitHub Repository](https://github.com/milosmns/circular-slider-android)
