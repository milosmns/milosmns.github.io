---
layout: post
title: Android · Troubles with Doze Mode
description: Testing and investigating Android's new power saver troublemaker - Doze Mode
date: 2016-09-08 15:00:00 +0100
image: '/images/posts/doze-mode.jpg'
tags: [dev, software, apps, android]
featured: false
---

#### Inspiration

My day job requires a lot of work on a serious and complex enterprise [Android VoIP app](https://www.counterpath.com/bria-enterprise), so I'm always eager to find out why our users might be experiencing issues with incoming calls or messages. After doing a lot of analysis and research, it turns out that most of the issues I was inspecting were related to [Doze mode](https://developer.android.com/training/monitoring-device-state/doze-standby.html). Since Android 7.0 (Nougat), Doze mode has [become more aggressive](http://www.androidauthority.com/android-n-doze-678982), and now it forces phones into killing network connections much earlier and way more often.

I prepared a sample app to verify some of the issues and check out what’s really going on.

#### Analysis

The app is located it its own [GitHub repository](https://github.com/milosmns/doze-test), check for more info in the README there. It's written in Kotlin (ooooo exciting), but that doesn’t impact anything related to Doze mode. 

You can simply test how Doze behaves without push by just running the app on your device. The app spins up a new thread and logs some stuff to the LogCat. It will let you know when the thread is a bit stuck due to other work, or when it fails to use the network completely. The worker in the thread is configured to ping `https://www.google.com/` every `INTERVAL` milliseconds (check `DozeLogger` for more info). The worker will also loop continuously until interrupted. Exiting the Activity using your `back` button will usually interrupt it, while exiting the Activity using the `home` button will usually keep the thread alive for a while longer.

After doing this test, you should be able to see that Doze mode kills **all** network traffic instantly when your phone turns it on. You can use commands from the README to manually go into Doze mode.

##### Push messaging

What \*should\* eventually wake up the app from Doze mode is a direct push message. Push messaging is now migrating towards FCM ([Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging)), therefore I implemented the push flow using the Firebase SDK. I suggest you do so too for your own tests.

To configure Firebase, just go to [Firebase console](https://console.firebase.google.com) and follow the instructions for creating a new project. Create a new account if you don’t have one already, of course. You don’t need hosting or any other stuff for this test. When you've created a new project, you can start testing **Notifications** from the website UI directly. I called my project “Doze Mode Test”, in case that means something to you. Follow the instructions that Firebase provides on the **Notifications** page, it is fairly straightforward to set up.

To send messages to your device, you will need to access your device's `Token`, which you can acquire directly by running my test app and clicking on the **Copy FCM Token** button. When copied, you should paste that token into Firebase Console's token field.

You can also try to use the security config generated in the `DozeTest/store/` directory from the repository, although you might experience some issue with certificates, keystore or other verification issues... so you might want to create your own credential documents instead. That should be fairly simple to set up from Android Studio, or read more about [app signing here](https://developer.android.com/studio/publish/app-signing.html).

Either way, your messages should be arriving now and you'll be able to test Doze mode with and without push messaging. Even though Doze mode works slightly different on Android 7.0 than on 6.0, the conclusion should be similar:

{:refdef: style="text-align: center;"}
![Doze mode results](/images/posts/doze-mode-results.png)
*Doze mode testing results*
{: refdef}

##### Additional notes

You can try [whitelisting your app](https://developer.android.com/training/monitoring-device-state/doze-standby.html#support_for_other_use_cases). **In theory**, this will let the app ignore Doze mode constraints in almost all cases. But the rule for bypassing Doze mode is getting stricter and stricter in each release, so it's unclear how much longer whitelisting will be supported.

This was a tought one to crack... I wish you happy further testing.
