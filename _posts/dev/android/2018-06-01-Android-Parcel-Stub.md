---
layout: post
title: Android · Parcel stub
description: How to stub the android.os.Parcel class
date: 2018-06-01 15:00:00 +0100
image: '/images/posts/package.jpg'
tags: [dev, software, apps, android]
featured: false
---

Did you ever wonder how to test any `Parcelable` data? Like a class implemented from the `Parcelable` interface, some kind of state class, or maybe something needs to be Parcelable inside of your custom Android Views... well, you would probably skip the testing altogether, right? It’s almost impossible to mock it properly and the implementation is simple enough not to make any errors anyway, right? Right?

Not a good idea. If you **add or edit** fields in your Parcelable's implementation class, it’s easy to forget to update the Parcelable implementation in all (3?) places. Reading about this issue, I found some bare-bones solutions, for example [this one](https://gist.github.com/Sloy/d59a36e6c51214d0b131)... but I eventually came up with a simple but more complete solution for this problem.

### My version

```kotlin
// Mockito is required for this to work
class ParcelFake {

  companion object {
    @JvmStatic fun obtain(): Parcel {
      return ParcelFake().mock
    }
  }

  private var position = 0
  private var store = mutableListOf<Any>()
  private var mock = mock<Parcel>()

  init {
    setupWrites()
    setupReads()
    setupOthers()
  }

  // uncomment when needed for the first time
  private fun setupWrites() {
    val answer = { i: InvocationOnMock ->
      with(store) {
        add(i.arguments[0])
        get(lastIndex)
      }
    }
    whenever(mock.writeByte(anyByte())).thenAnswer(answer)
    whenever(mock.writeInt(anyInt())).thenAnswer(answer)
    whenever(mock.writeString(anyString())).thenAnswer(answer)
    // whenever(mock.writeLong(anyLong())).thenAnswer(answer)
    // whenever(mock.writeFloat(anyFloat())).thenAnswer(answer)
    // whenever(mock.writeDouble(anyDouble())).thenAnswer(answer)
  }

  // uncomment when needed for the first time
  private fun setupReads() {
    val answer = { _: InvocationOnMock -> store[position++] }
    whenever(mock.readByte()).thenAnswer(answer)
    whenever(mock.readInt()).thenAnswer(answer)
    whenever(mock.readString()).thenAnswer(answer)
    // whenever(mock.readLong()).thenAnswer(answer)
    // whenever(mock.readFloat()).thenAnswer(answer)
    // whenever(mock.readDouble()).thenAnswer(answer)
  }

  private fun setupOthers() {
    val answer = { i: InvocationOnMock ->
      position = i.arguments[0] as Int
      null
    }
    whenever(mock.setDataPosition(anyInt()))
      .thenAnswer(answer)
  }
}
```

You would use it just like a normal Parcel -- get an instance by calling the static `obtain()` method on that class, write and read using the Parcel's well-known class methods.

Happy stubbing! 😬
