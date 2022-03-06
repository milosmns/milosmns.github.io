---
layout: post
title: SMS Global · A bad review for a terrible business
description: How SMS Global let me down and cost me time and money
date: 2015-10-11 15:00:00 +0100
image: '/images/posts/typing-on-phone.jpg'
tags: [op-ed, apps, ux, review]
featured: false
---

#### Where I'm coming from

I use my computer a lot. In fact, I have a bunch of different computers (laptops, desktops, servers) and my job requires me to be connected more or less all the time. That being said, I've been searching for a way to sync all of my data across my machines: stuff like SMS, calls, apps... basically everything. Most of the things I need can be done easily using some kind of fancy new app or a new service.

I decided to give it a shot through custom scripting and using **SMS Global**. This is the experience I had.

### In the beginning...

I created an account on [SMSGlobal](https://www.smsglobal.com) a few months ago because I needed a service to send SMS from, even when I’m away from my phone (in a different country or just need a custom “From" header in the message). SMS Global promised to give me all of that for a fee.

I paid quite a few bucks for the service (keep in mind that they now have my credit card and personal data). I tested the service on a few networks, and **there were problems**. I couldn’t set the “From” header properly for all SIM providers worldwide. It worked only for one of the 5 telcos I tested with. Instead of at least setting my name as the sender, they set some strange foreign number that just confused people...

There we go, disappointment #1.

### More problems

I wrote to their support about this issue, and they told me that they can’t do anything. The response came 2 weeks too late, of course. That's my disappointment #2. Even though I felt like they stole my money and misled me into believing that their service is truly "global", I stopped complaining about this issue and also stopped using the service for a while.

{:refdef: style="text-align: center;"}
![The problem is me](/images/posts/reaction-my-problem.gif)
{: refdef}

A few weeks had passed (maybe even months?), and I needed to check in again and see if it’s still working to use in another project. So, I go to the login page from my phone, log in, and then see this page:

{:refdef: style="text-align: center;"}
![Broken layout](/images/posts/sms-global-console.png)
*Broken, non-responsive layout*
{: refdef}

Some problems I notice being here:

  - I can’t possibly know the actions these red icons perform
  - The apology is not accepted. Tell me what exactly is wrong!
  - The menu button is not working at all (I'm on the latest Chrome and the latest Android OS)
  - A huge space-eating warning on the top about a mysterious threshold, one that I did not set myself

Disappointment #3. Moving slowly into anger. So we have a meaningless message... fine, let’s see what’s on the bottom.

{:refdef: style="text-align: center;"}
![Random errors](/images/posts/sms-global-error.png)
*Random coded error*
{: refdef}

Wow, ok. Let’s analyze that too.

  - **Access denied**: it means that I did log in? But I can see my name using the mysterious human icon... still, I can’t access the home page?
  - **MVC**: Model View Controller, a popular concept in software engineering? Seeing this means that there is no message to display, so the server just pumps out the error directly from the program. Really concerning to see in this day and age
  - **default.messaging.send-to-number**: I am guessing that this is the page I can’t access? Who knows...

This makes no sense to me. I'm getting stressed. Let's see what else... I try to find the support button on a non-working page. It takes like 5 minutes, and I build user interfaces for a living.

Disappointment/Annoyance #4: on the support page, it took me 3 more minutes to find the login button. Why do I need to log in? Well, because they logged me out again for some reason, of course. I wrote about the problem, explaining that I have money in that account. Not that I care about getting my money back (it's not millions), but it’s just annoying that they don’t want to give me any information except the dumb coded messages! It's like talking to the Google Play Console support.

### Final phases

I got a response (2 more weeks later)!

Here it is:

{:refdef: style="text-align: center;"}
![Bad email response](/images/posts/sms-global-email.png)
*Terrible customer support*
{: refdef}

Annoyance/Frustration #5: wow, I have to call them?! Call them, on the phone, which is btw in a different country code. NO. I ask again about the issue, they should explain the problem just as easily over email.

The second answer was totally ridiculous. But they can communicate over email after all. They said that I was using an "unfamiliar" name in the “From” header, which then blocked my account without telling me. Wow. Just wow. Frustration #6. **Of course I used a different name!** That's the point, isn't it?! When I write messages to my mom, she knows who it is. But when writing to a customer or syncing data to another server, how the hell would the other side know who is writing and about what?! Sometimes I need to write the company/project name to some people, and first name to other people, even nickname to some. This is what they were selling in the first place.

#### Conclusions

First they don’t know what’s wrong and I need to call them, then suddenly they know everything. Then they know contents of all of my messages? Wow. How far does this go?! And the service isn’t even working for me properly. I complained again saying that I want my account removed immediately, deleting all of my data from their servers (as it is clearly not encrypted). I also want my money back, it's literally fraudulent behavior!

And it’s not like they are having [amazing reviews](http://www.productreview.com.au/p/smsglobal.html?sort=rating_low). They desperately need new, satisfied customers. And failed, again. Their last reply was the best: (Frustration #7) after everything that happened, they told me to delete the account from the home page when I log in... the home page, THAT'S NOT WORKING FOR ME! Damn it.

{:refdef: style="text-align: center;"}
![Angry reaction](/images/posts/reacion-crazy.gif)
{: refdef}
