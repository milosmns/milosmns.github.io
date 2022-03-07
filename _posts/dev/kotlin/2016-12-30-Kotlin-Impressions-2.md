---
layout: post
title: Learning Kotlin! Adventure, part 2 of 2
description: Playing around and getting to know Kotlin, a relatively new programming language for the JVM and Android
date: 2016-12-30 15:00:00 +0100
image: '/images/posts/kotlin-island.jpg'
tags: [dev, software, apps, android, kotlin]
featured: false
---

### Previous work

Before we start, I want to invite you to read the first part of the series here on the site. If you read that, you'll now be glad to know that this part is a direct hands-on development overview of how I made an Android app using only Kotlin and the standard Android SDK.

If you’ve read this far, it probably means that you’re interested in using Kotlin as your primary programming language on Android (or another platform). I'd say you're also probably right for taking action “against” using Java. Before diving in any deeper here, take a look at [this awesome talk](https://realm.io/news/gotocph-hadi-hariri-kotlin-ready-for-production) by [Hadi Hariri](https://twitter.com/hhariri), just to get a better sense of where things are now with Kotlin and JetBrains.

So far, you’ve seen the language and my somewhat fanboyish introduction to Kotlin. Now, let’s get to the real stuff. Kotlin is today at [version 1.0.6](https://blog.jetbrains.com/kotlin/2016/12/kotlin-1-0-6-is-here), introducing some new and helpful language constructs, plus some overall stability and bugfix improvements. Still, even though it’s considered "stable" and production-ready by the language authors, many people are still holding off on actually releasing their apps to the public with Kotlin inside. I just want to say that **it's fine**. What a lot of teams are doing is writing Unit and Integration tests using Kotlin. From my point of view, that’s a really easy way of transitioning to Kotlin and learning the language, but still keeping stability in the main product you are developing. After I played around with Kotlin in my free time, I decided to do one whole app (including tests and app code) in Kotlin.

### Running with it

You’re a developer, so it's likely that you have a pet project or idea in which you try out all kinds of new stuff you stumble upon. For me, that pet project is **Timecrypt** (now deprecated in favor of other stuff). It's my idea of a free, open-source, messaging API that allows users to send, schedule, read and self-destruct text messages over the Internet, through encrypted channels. Basically, what it does is just encrypt (optionally using a custom passphrase) and store messages on a server, until they are loaded a specific number of times, or a specific deadline date is reached. The receiver's side is the only one who can decrypt the messages. Essentially, it’s expected of you to provide the server implementation following the specified API specification (or use the provided demo implementation) -- and your ready to run it. I wanted to create a Timecrypt Android app for a while now, and since I was preparing to test out Kotlin in a real-world app, this was a no-brainer.

A few weeks after Kotlin 1.0.3 was published ... a decision was made. Timecrypt, get ready to meet Kotlin!

#### The first phases

The first thing I did was similar to what other people do with Kotlin today -- create some tests. In order to use Kotlin in your project, you need to import Kotlin’s standard library (`stdlib`) and teach Gradle how to compile Kotlin -- here is a [great tutorial](https://kotlinlang.org/docs/tutorials/kotlin-android.html) to quickly get started.

After Kotlin is configured, you can start writing tests. What should I test first? Since I already had the API defined, my first step was to build an HTTP module that would directly use my REST API. I did that using [Retrofit](https://square.github.io/retrofit), of course, and it was a good and simple choice that allowed me to focus on other, more important stuff. The networking module, Retrofit, and my custom-built controller are in the `v2/api/` package (in case you want to see the source later).

The three simple Kotlin interfaces I had to create for my HTTP **responses** were:

```kotlin
// Comes from the the ‘/create’ endpoint
class CreateResponse(
  val id: String?,
  @Json(name = "status_code") val statusCode: Int
) : TimecryptResponse

// Comes from the ‘/read’ endpoint
class ReadResponse(
  val text: String?,
  val title: String?,
  val views: Int?,
  @Json(name = "lifetime") val destructDate: String?,
  @Json(name = "status_code") val statusCode: Int
) : TimecryptResponse

// Comes from the ‘/is-locked’ endpoint
class IsLockedResponse(
  @Json(name = "locked") val isLocked: Boolean?,
  @Json(name = "status_code") val statusCode: Int
) : TimecryptResponse
```

All of them extend the common `TimecryptResponse` class -- a simple marker interface so that I can use a common reference in the `TimecryptController`. There's been some talk about sealed classes to allow this out of the box, but there's still nothing official.

You would maybe think now: “Okay, so these come in from the server to me, mapped into Kotlin objects, but essentially they are just plain JSON objects, right?” -- and you would be correct, yes. In JavaScript, you wouldn’t need to create these classes, as JSON objects are natively and directly accessible from JS code. Here we needed Retrofit and its Kotlin support to have it handled automatically. Next thing we need is a **message** class -- the one you would fill with data while creating or reading a message -- and similar to these 3 responses from above, it is a simple Kotlin representation of a JSON object.

What I came up with is:

```kotlin
class TimecryptMessage(
  var text: String,
  var views: Int = 1,
  @Json(name = "lifetime") var destructDate: Date? = null,
  @Json(name = "email_to") var emailTo: String? = null,
  @Json(name = "email_from") var emailFrom: String? = null,
  var title: String? = null,
  var password: String? = null
) : Parcelable
```

I'm thinking that `data` classes might be more appropriate here and above... but let's see later.

Now we have (very declaratively) created all these small components required to make the HTTP requests to the REST API. What we are still missing is the “meat”, the module that actually makes the requests. 

Luckily, this is also super-simple using Kotlin and Retrofit:

```kotlin
interface TimecryptRestApi {

  @POST("create")
  fun create(
    @QueryMap values: Map<String, String>
  ): Call<CreateResponse>

  @GET("is-locked")
  fun isLocked(
    @Query("id") id: String
  ): Call<IsLockedResponse>

  @GET("read")
  fun read(
    @Query("id") id: String,
    @Query("password") password: String? = null
  ): Call<ReadResponse>

}
```

If you read the Retrofit docs, you’ll see that HTTP URL params are passed in using `@QueryMap`, so that’s why I used it. To convert a message to this format, I used a simple utility method from my `Utils` class, located in the same package. Yes, I could have done it differently (using `Moshi` or `GSON`, for example) but this was much faster for me personally and I didn’t want to waste any more time on the networking module.

So there you have it. With only several lines of code and a few simple structures, I have a fully working HTTP REST client ready to go. Now I can test it!

One more technical thing I had to do is create a developer-friendly API, open to the UI layer. Like a domain-level component.

I could have done one of these things I thought of at the time:

  1. Create the Retrofit instance inside of each Activity (or use a dependency injection mechanism to create a singleton) -- then use RxJava or similar library to do asynchronous work using `TimecryptRestApi`. This is bad for obvious reasons (breaking SOLID in a few places)
  2. Manage a single Retrofit instance and do all asynchronous work inside a custom-built `TimecryptController`, or something like that. Repository?

I chose the second option as it seemed less cryptic to the users who never encountered any of these libraries, and also it doesn't break SOLID as much. I called it "Controller" even though it's really a repository... but it doesn't matter for now, I just want to move on.

#### The main dish

Now that my controller and my network module are ready, it’s time to get to the UI stuff. I'm skipping presenters and view models because this is still not well defined anywhere by Google.

Timecrypt for Android has several UI states:

  1. **No message** -- user hasn’t entered any text yet
  1. **Creating message** -- user is typing and setting up the message
  1. **Message created** -- user’s message is stored on the server
  1. **Reading message** -- user arrived to the app trying to read a message
  1. **Unlocking message** -- awaiting a password for the message

I decided to merge the first two states into one, and also the last two states into one as well, creating the following structure:

**CreateMessage activity (states 1 and 2)**

This activity is responsible for creating new messages. It uses a `ViewPager` to display the two pages side by side. It displays the “No message” UI initially, then it displays the full “Prepare message” UI when any text is entered into the text field. Fragments for the pager are all located in the `pages` package.

The **Create** button shows a “please wait” UI while we create the message on the server. When done, the app will show the `LinkDisplay` activity with the message information so that users can share it further.

**LinkDisplay activity (state 3)**

This activity is responsible only for displaying information about the message that has just been created by the Timecrypt server. Users can copy, share or view the message from here. The **Create** button moves the user back to `CreateMessage` activity

**ReadMessage activity (states 4 and 5)**

This activity is responsible for loading and displaying a message from another source, e.g. when someone sends you a link to the Timecrypt message they created. It also handles the password entry flow if the message received was locked by a password. The **Create** button here moves the user back to `CreateMessage` activity. It’s shown only when the message is properly unlocked. The **Unlock** button sends the entered password to the Timecrypt server to unlock the message. Users will never know if they entered a wrong password, they will just get a messed up message if password is wrong. This page is shown only if the message is not yet unlocked.

All of the layouts are fairly simple, I wouldn't go to deeply into it. 

There's one really interesting Kotlin thing to note here -- I wanted to automatically notify all listeners when my message property changes inside of any fragment, so here is a sample of how that would work:

```kotlin
// a Kotlin property with an overridden setter so that I can notify listeners
// also, the ‘message’ property here has a backing field
private var _message: TimecryptMessage = TimecryptMessage("")
override var message: TimecryptMessage
  get() = _message
  set(value) {
    _message = value
    // notify only there are listeners
    if (listeners.size > 0) {
      onMessageUpdated()
    }
  }
```

Fun and easy, right? Attaching a listener to a class property... mind blown!

Wait, one more fun thing. How do I notify my listeners exactly? All listeners are stored by the emitter interface's implementor, keeping a reference to the listener list.

The emitter function notifying them is:

```kotlin
// ‘event’ is a function taking a listener and returning Unit (void in Java)
// then we do the ‘forEach’ loop, invoking that function on each listener
fun notifyListener(event: (OnMessageChangedListener) -> Unit) =
  listeners.forEach(event)
```

Whaaaaaatttt?? How does that work?!

  - These are called higher-order functions, basically passing a function instance around

Here is an example of how I use the `notify` function with a shorthand lambda expression when the message changes:

```kotlin
notifyListener { it.onTextInvalidated(true) }
```

I think you'll agree that in today’s state of Java compatibility on Android this simply **cannot be done**. Even if it's possible using retro-lambda and similar tools, it would still be done using multiple classes, interfaces and callback functions... I'd rather just give up and use a 3rd-party event bus that is generic enough.

Okay, enough hate for Java 😬

Another interesting function (and I really can’t mention everything here) is the "toggle visibility" shorthand for Views. Here it is:

```kotlin
protected fun View.toggleVisibility() = 
  if (visibility == View.VISIBLE) visibility = View.GONE
  else visibility = View.VISIBLE
```

Boom, done. You can now call `toggleVisibility()` on each View, anywhere! Again, something that would be impossible in Java.

#### Final touches

What about page/fragment management? Well, since I use an overridden variant of the `ViewPager` to be able to toggle touch handling, it’s only a few lines of code. I won’t write anything more about it.

My `SwipeAdapter` implementation that I use with it is also an emitter, but it requires more functionality than just that. It also serves as a relay between the activity and all internal pages. It can forward or stop events passing between any two activity/fragment components, and it also manages the caching and destruction of pages. Probably it shouldn't do all of this, but I wanted to demonstrate the power of Kotlin!

Here is everything that my adapter implements and requires for construction:

```kotlin
class SwipeAdapter(
  listener: OnMessageChangedListener,
  message: TimecryptMessage,
  val manager: FragmentManager,
  override var listeners: MutableList<OnMessageChangedListener> = mutableListOf()
) : FragmentPagerAdapter(manager), OnMessageChangedListener, OnMessageChangedEmitter
```

But it's so easy to declare classes with constructor arguments!

Next, to actually construct the adapter, an activity or a DI container needs to do something like this:

```kotlin
val swipeAdapter = SwipeAdapter(this, message, supportFragmentManager)
```

Again, really easy and concise.

There's more!

```kotlin
import kotlinx.android.synthetic.main.activity_create_message.*
```

Do you know what that does? It converts your View ID resource names into **class properties**, doing the `findViewById()` search only when you use the property for the first time. It literally removes all of the View finding boilerplate! You can read more about it [here](https://kotlinlang.org/docs/tutorials/android-plugin.html).

And the last snippet for this post is the tag String for the Android logger:

```kotlin
private val TAG = ReadMessageActivity::class.simpleName!!
```

Ok, I agree, that’s a bit ugly.

### To recap

Kotlin really feels powerful. It's short and to the point, while allowing a lot of things. It made my app a lot smaller and a lot more readable. It also has a small footprint, and it’s easy to get used to. It’s also fully interoperable with Java. It makes writing programs a real joy (again?).

It’s ready for production, so let’s start using it already! 😬
