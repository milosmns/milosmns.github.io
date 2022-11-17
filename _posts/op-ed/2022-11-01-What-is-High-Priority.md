---
layout: post
title: What is High Priority?
description: >
  "That doesn't matter!" – it's said far too often, isn't it? But did you know that we often don't consider facts and conditions when we think about priorities?
date: 2022-11-01 16:00:00 +0100
image: '/images/posts/prism-crystal.jpg'
tags: [op-ed, time, management, organization]
featured: false
---

### The <font color="#F88">Time Management</font> Series

This post is just one part of my [Time Management](/2022/11/01/Time-is-of-the-Essence) series. I really recommend you read the whole series if you have time, but I'll do my best to make this part self-contained.  
**Important disclaimers** are also included there.

-----

## A bullet-proof framework

#### 🎯 &nbsp; About goals…

More controversial opinions: ✅

There are a few things I consider when setting goals for myself and my organization[s]:

1. The _more responsibility_ I bear for my decisions, the _less_ often I have to make decisions. Make sure those choices are good 
2. I can do things right in many different ways, often _without_ going through the _known/proven steps_. Skip steps when possible 
3. I've become _brutally honest_ with myself about my capacity and time commitment. This is to the point that I _give up_ on most (90%) of my ideas and external requests. This is good, be transparent and reject things

**What do you disagree with the most?!**

Either way, I think I can justify most of the things I just wrote, even though my framework isn't great. 😄 But it's a good starting point if we're looking for a reliable algorithm to prioritize tasks, I think.

So what are we looking for?

```kotlin
fun findPriorityItem(items: List<WorkItem>): WorkItem {
  // FIXME: This is what we're looking for
  error("Too hard to implement")
}
```

#### 🌱 &nbsp; The basic framework

Visualizations are nice, but let's also clarify. Remember that all classifications here are **relative** and not absolute, we're always comparing work items to other work items on the table.

{:refdef: style="text-align: center;"}
![Priority Matrix](/images/posts/time-management-priority-table.png)
*The Priority Matrix (Nike don't sue me)*
{: refdef}

**1. Urgent, but _Not_ Impactful**: "Just do it."  
These are the things I really don't want to do, because I don't think they're important (yet). But these things tend to escalate quickly if ignored. For example, my day-to-day work includes updating security libraries, understanding a rare bug in the Canary deployment, investigating a sudden drop in analytics events or a spike in costs, approving access requests, etc. I usually force myself to do these things right away because they get done quickly and don't mess up my schedule at all. Waiting can cause them to be moved to the next category here, which I don't want.

**2. Urgent and Impactful**: "This is your next task!"  
There's nothing more impactful or urgent than these things. If it's a problem, it can't escalate any further because it's already at its worst… an example is a critical bug in our production environment. If we're referring to new tech or product initiatives, that's the one that will benefit your users the most… for example, the ability to edit messages in a chat app, or the ability to tip the courier in a food delivery app. These are things that usually take a lot of time to implement, but are of great benefit to both the users and our organization.

**3. Not Urgent, but Impactful**: "Put on the Radar"  
You know this will have a big impact, but you're not ready for it. You don't know where the market will go, how technology will evolve, who'll block you or unblock you… but you know for sure that it's going to be a big deal. Some examples that come to mind are: try a new programming paradigm (reactive and functional programming), try a new monitoring tool (ELK stack and Prometheus/Grafana), cross-platform technology, etc.

**4. _Not_ Urgent and _Not_ Influential**: "Decline!"  
Nothing and no one is forcing you to act quickly. The impact isn't clear, or it's clear that the impact is small. Some examples that come to mind are: Adding or removing an app component that's not been analytically captured or analyzed in user research (i.e., the impact is unclear), adding or changing a feature for the sake of change (i.e., the impact is potentially negative), refactoring a rarely used system or service (i.e., the impact is minimal), etc. So the point isn't that this shouldn't be done at some point… it should… it just doesn't have enough impact compared to other things on the table.

#### 🙊 &nbsp; Audience questions

**<font color="#F88">—</font> What would you do if you couldn't make your own decisions about priorities?**  
_(you ask)_

I don't make those decisions on my own anyway. And, of course, I don't always apply this basic framework to everything. It's just a good **starting point** for setting the right priorities, if you're willing to be honest with yourself and aware of your environment. I still ask my colleagues for feedback, talk to the teams I work with, interview stakeholders, cost center managers, product leads… and finally get everyone's input before I make a decision.

It's always good to have data at hand, because without data it's hard to argue with people holding more "power" than you. In my personal life, I do more or less the same thing - my wife is my main sparing partner, so it's not a solo effort here either.

💭 &nbsp; Reminder: _Progress is impossible without change, and change is impossible without someone driving it_.

**<font color="#F88">—</font> What if I have too many things in one of the categories?**

Well, I usually just focus on the first two categories. If there's too much going on in one of the first two categories, I apply the same prioritization process within the crowded category.

💭 &nbsp; Reminder: _When everything is important, nothing is important_.

**<font color="#F88">—</font> How do you know if you have time for something?**  
**<font color="#F88">—</font> How do you justify _not_ doing everything that comes your way?**

I plan getting things done backwards, even though I realize I can't plan for all the tiny details. But most things can be planned backwards, because with enough experience it's possible to anticipate and react to problems before they occur.

**What does this mean in practice?**  
Imaginary example. Let's say we're working on user proximity detection and reporting with GPS from your app, trying to detect clusters of users. We're now at **November 1**, but let's assume we want to complete this initiative before the end of January.

Starting backwards from **February 1** (with imaginary dates, estimates, and milestones): 

  - **Jan 31**: Impact analysis ready in BI 
  - **Jan 15**: Clients rollout complete 
  - **Jan 02**: Clients rollout started 
  - **Jan 01**: Backend big bang rollout completed
  - **Dec 24**: Development work completed and waiting for release 
  - **Dec 10**: Code freeze due to upcoming holidays
  - **Dec 02**: Development work begins
  - **Dec 01**: Legal, security and privacy teams approve changes (GDPR, CCPA, LGPD)
  - **Nov 15**: UI/Design is complete and engineers approved
  - **Nov 02**: UI/Design work started
  - **Nov 01**: UX work complete and UI/Design work started

It appears that there's no (or little) time for:

  - Competitor and market analysis
  - Product research and feedbacks
  - User research and interviews
  - Stakeholder feedback and approval
  - Assignment of data and cost centers
  - Understanding the impact on local operations teams
  - Potential technical and non-technical revisions
  - Engineering learning and understanding of the problem space
  - Other things I can't think of right now…

Not to mention, the team doesn't sit idle for weeks waiting for approvals. Engineering resources are scarce and unchanging. If 6 things are running in parallel and people are constantly jumping between issues, some of those issues are bound to be delayed. All the scheduling combined with changes in priorities has a big impact on the final roadmap.

**<font color="#F88">The Final Decision</font>**: Either discard this or something else (keep only the highest priority things)!  

Thanks to this process, I can communicate planning issues clearly and transparently, and it's clear why most things need to be rejected.

💭 &nbsp; Reminder: _Optimize to get a few things right instead of optimizing to look busy_.

**<font color="#F88">—</font> If your team had a 5-year roadmap, what would you do?**

This is a tough question. A long roadmap is basically a long-term product commitment, and that's a good thing for a product. Unfortunately, anything long tends to accumulate risk over time, and Agile/Lean organizations are generally better at risk management. I am referring to the good old Agile risk management chart.

{:refdef: style="text-align: center;"}
![Traditional Risk Management Chart](/images/posts/time-management-risk-traditional.png)
*Traditional risk management chart*
{: refdef}

{:refdef: style="text-align: center;"}
![Agile Risk Management Chart](/images/posts/time-management-risk-agile.png)
*Agile risk management chart*
{: refdef}

To combat these risk challenges and ensure we're better serving our stakeholders, most teams I work with have recently implemented a **[Continuous Planning](https://www.umt360.com/blog/continuous-planning)** process. Of course, every implementation of this process is different. But from my perspective, I see it as more agile, an iteration of the agile approach to risk reduction applied to the entire roadmap (rather than a single product).

For each individual case, I'd recommend looking at product release risk history, launch cadence, other [DORA metrics](https://cloud.google.com/blog/products/devops-sre/using-the-four-keys-to-measure-your-devops-performance) and similar data points to decide which process is best. It may be that a long roadmap is better for the team, although that's rarely the case.

The best read on this so far:

  - 🎧📱📚 &nbsp; [The Phoenix Project](https://www.amazon.com/The-Phoenix-Project-audiobook/dp/B00VATFAMI)

{:refdef: style="text-align: center;"}
![Prioritization](/images/posts/time-management-priority.png)
{: refdef}

-----

## Tools and hacks

#### 🔕 &nbsp; When you're busy, you're busy

This goes hand in hand with the basic framework I described above. Again, engineering resources don't just simply grow when you need them, so it's not possible to make up engineering time that doesn't exist. That's why I think it's very important that people in the environment understand the constraints of each team member… to be clear, I have limited time to work, limited team resources, and a pretty fixed schedule. This framework ensures that I finish my work on time (or almost on time), which in turn guarantees that I have time for a life outside of work as well.

I'm a firm believer that all requests, inquiries, and questions (personal or professional) deserve a response -- at least to communicate that I'm busy. It takes almost no time to reply _"I'm busy right now, let me get back to you later"_, so I try to at least do that whenever possible. But if I'm having a really busy day, I'll set my [Slack status to busy](https://slack.com/help/articles/214908388-Pause-notifications-with-Do-Not-Disturb) -- then the messages often don't come at all, because people immediately see that I'm busy.

{:refdef: style="text-align: center;"}
![Slack Profile](/images/posts/time-management-slack-profile.png)
*Example of a Slack profile with DND mode and Calendar status*
{: refdef}

#### 📅 &nbsp; About meetings…

It's rough and meetings can be a huge productivity killer. The best meeting is **no meeting**. And by that I don't mean you turn down meeting invitations for no reason -- I mean you weigh whether or not you really need a meeting. Maybe you can delegate it to someone, maybe you don't have an agenda, maybe you don't have topics to discuss, or maybe it can be a chat message… then it's okay to skip it. Meetings without a clear agenda (in the title or description) shouldn't happen anyway, because it's impossible to prepare for them, and therefore much of the meeting is spent learning about the context -- rather than problem solving.

To reduce the number of meetings in a day, I use Google Calendar's **[Focus Time](https://support.google.com/calendar/answer/11190973)** and reduce my **[Interviewing Schedule](https://support.google.com/calendar/answer/10729749)** availability. At the same time, my **[Work Hours](https://support.google.com/a/users/answer/9308669)** are also always enabled so I don't get meetings after a certain time of day. My lunch break is also scheduled every day. This setting automatically rejects so many meetings that I'm worried to give the exact number here. 😅

##### Aligning team schedules

Other than that, all the teams I work with have a **Meeting-free day** and an **"Agile day"**. The former is pretty self-explanatory -- a clear blocker in the calendar for the whole team, throughout the day -- while the latter is something we've come to after experimentation. For our Agile day, we try to do all agile ceremonies except the daily standups on a single day, for example every other Monday. This involves meetings like product grooming, tech refinement, retrospective, roadmap and cost risk reviews, etc. Having a dedicated Agile day ensures that engineers have few interruptions during the week and still have all the ceremonies that ensure a steady flow of high quality work.

##### Going the extra mile

I invite all participants and **heavily** <font color="#8F8">color</font> <font color="#AAF">code</font> my calendar, both for my personal and work calendar. If it's not on the calendar, it doesn't happen. This may seem like too much, but it really helps me prioritize and plan my days. Check it out:

{:refdef: style="text-align: center;"}
![Calendar](/images/posts/time-management-calendar-grouped.png)
*Color-coded calendar for a real week in September*
{: refdef}

So I can see **at a glance** what my day will look like. I even import my personal calendar into the same view (with a different color) to see what's coming up after work, because sometimes I go to the office to work when my after-work event is closer to the office.

##### Other tips

At the end of each day, take 15 minutes to look at your calendar for the next day and discard anything you won't do. Try to balance different colors that day. Trust me, you don't want to do the same type of thing all day… variety is good.

And since time is usually at a premium, it's best to schedule a set time on your calendar for your weekly or bi-weekly recurring 1:1 meetings. That way, you can be sure you'll always have a window of time to talk about growth and sensitive issues, whether it's with your direct reports or your supervisor.

{:refdef: style="text-align: center;"}
![Busy](/images/posts/time-management-busy.png)
{: refdef}

-----

## In conclusion…

It's really hard to prioritize, and I can't stress enough that there's no silver bullet. As we part ways here, I'd like to leave you with a nice quote from the man who restructured Intel into a successful company:

> My day ends when I am tired and ready to go home, not when I'm done. I am never done.
> There is always more to be done, more that should be done, always more than can be done.
>
> <cite>Andy Grove</cite>

I think what he says here is counterintuitive; he's not saying that we should work all day, but rather the opposite. We should aim to do what we can in high quality and then go home. That's a good attitude to have.

Recommended reading (by the same author):

  - 🎧📱📚 &nbsp; [High Output Management](https://www.amazon.com/High-Output-Management/dp/B08Z8K64S2)

{:refdef: style="text-align: center;"}
![Thank you](/images/posts/time-management-pray.png)
{: refdef}

-----
