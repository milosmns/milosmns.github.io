---
layout: post
title: Android · Actual Number Picker
description: A free UI element for horizontal number picking, resembling a top-down look of a wheel
date: 2015-12-15 15:00:00 +0100
image: '/images/posts/actual-number-picker.png'
tags: [dev, software, android, open-source]
featured: false
---

I wrote a somewhat decent View as a replacement for the huge native number picker. I don't find the default one very nice to use or look at...

The properties are easy to change and set up:

```xml
<me.angrybyte.numberpicker.view.ActualNumberPicker
  app:bar_color="@android:color/white"
  app:bar_width="1dp"
  app:bars_count="26"
  app:controls_color="@android:color/white"
  app:draw_over_controls="true"
  app:draw_over_text="false"
  app:fast_controls_color="@android:color/darker_gray"
  app:highlight_color="#FFFF3040"
  app:max_value="100"
  app:min_value="0"
  app:selection_color="#A0FF3040"
  app:show_bars="true"
  app:show_controls="true"
  app:show_fast_controls="true"
  app:show_highlight="true"
  app:show_text="false"
  app:text_color="@android:color/white"
  app:text_size="16sp"
  app:value="50" />
```

Anyway, here’s the source code:

  - [GitHub Repository](https://github.com/milosmns/actual-number-picker)
