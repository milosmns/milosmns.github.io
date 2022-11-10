---
layout: post
title: Backlogs are Evil
description: Are you getting things done? Or are you getting stuck trying to get things done? Maybe you're jumping back and forth between topics? Maybe we had the same problem.
date: 2022-11-01 15:00:00 +0100
image: '/images/posts/car-jam-queue.jpg'
tags: [op-ed, time, management, organization]
featured: false
---

### The <font color="#F88">Time Management</font> Series

This post is just one part of my [Time Management](/2022/11/01/Time-is-of-the-Essence) series. I really recommend you read the whole series if you have time, but I'll do my best to make this part self-contained.  
**Important disclaimers** are also included there.

-----

## The Black Hole Backlog

Clickbait title: ✅  
Controversial opinions: ✅

But let's at least be on the same page: I define **backlog** here as a **large collection of pending and uncompleted work**, referring to both personal life backlogs, team backlogs, and individual/internal work backlogs.

Want to read something interesting though? I have 0 (zero) TO-DO lists and don't use TO-DO software at all. There are other things I do to compensate, but my productivity hacks all boil down to avoiding TO-DO lists.

#### 🎯 &nbsp; The Core Issues

You've probably heard it before: _"Just put that in the backlog"_… and I can't stress enough how bad it is to treat your backlog this way. If you treat your backlog like a black hole, it actually becomes a black hole. A **black hole backlog** is super hard to search, the quality of backlog items is low, it's impossible to skim items quickly, there's no way to get a good overview of priorities, work motivation drops significantly -- and ultimately, you need a professional tool to manage your backlog.

#### 🧽 &nbsp; Refinement Issues

I assume that in engineering you go through (at least) a three-tier refinement and prioritization process: product, engineering, stakeholders. But now that your backlog is a black hole, your refinement process becomes much longer and more complex. Backlog refinement and prioritization process is a common cause of stalled workflows.

#### 📉 &nbsp; Quality of Work Items

In general, I find that [Scrum](https://www.atlassian.com/agile/scrum) works better for new teams/products, while [Kanban](https://www.atlassian.com/agile/kanban) works well for more stable teams/products -- but with both of these popular approaches, your backlog is supposed to be optimized, and the tasks need to be well sized and defined. A black hole backlog hinders delivery performance in both cases because it's basically a dumping ground where ideas and requests disappear.

#### ✨ &nbsp; Innovation Cannot be Planned

To keep motivation at a high level and make sure you don't lose the thread of brilliance, it's important to pursue inspiring and innovative ideas immediately… rather than in 4-6 months down the road. Huge backlogs and roadmaps force us to put off innovation. If you put brilliant ideas in a black hole backlog, it's almost certain that they'll never be implemented. And what's worse, your team is smart and will quickly realize that your backlog is a black hole -- so now, if they have a good idea, they'll naturally be hesitant to throw their good idea into the black hole. As a result, those ideas don't even show up, in the good old false assumption that there's not enough time.

#### 🐢 &nbsp; Always Starting, Never Finishing

With black hole backlogs, we often can't focus enough on what's important. An abundance of pending, uncompleted work makes blocked work items a low priority. In this way, new work can be constantly started while the blocked work isn't completed. Ideally, a blocked task should be completed (or discarded) as soon as possible… after all, blockers are a big reason why we do daily standups in the first place. Black hole backlogs give the impression that there's always something else important to do, so blockers go unaddressed for a long time.

#### 🚶🏼‍♂️ &nbsp; Personal life

On a personal level, I see black hole backlogs in my chore lists, such as: pick up this item from there, clean up this area, have this item delivered, buy this item, etc. I believe the same principles of backlog management should apply to personal items, provided you're willing to put in the effort necessary to streamline your workflow.

{:refdef: style="text-align: center;"}
![Black Hole](/images/posts/time-management-black-hole.png)
{: refdef}

-----

## Let's fix that!

#### 🧠 &nbsp; The Solution: Change your Work Style

An obvious goal, right? 😄 But it's not so obvious how to achieve it. It's a hard problem, and in my experience it's mostly related to prioritization, scheduling, communication, delegation, and more… primarily prioritization I believe. I've found that it's almost never related to the number of things you have to do.

> Backlog management issues don't scale linearly with the number of things you have in the backlog
>
> <cite>You heard it here first</cite>

I've written about all kinds of tweaks in the other parts of this series, so be sure to check them out.  
If you don't have time to read through the rest of the series, I can offer you some mitigation strategies that will have an almost immediate impact.

#### 1️⃣ &nbsp; Delivery Improvements

If you're working in a Kanban environment, you're in luck, because **[Work-In-Progress limits](https://www.atlassian.com/agile/kanban/wip-limits)** are really helpful. But WIP limits only address the consequence here, not the cause, so treat them as such. On the other hand, if you're using Scrum, you might try focusing on limiting or removing changes to the Sprint Backlog during a Sprint. In most Scrum implementations, the engineers are the Sprint Owners and they're **[the only ones allowed to change the Sprint](https://scrumguides.org/scrum-guide.html#artifacts-sprintbacklog)** while it's still running.

For my personal life backlog, I tend to divide the work into sprints that last **no longer than 2 hours** -- that way I have enough time to get things done, but I won't waste a whole day on chores. I break this rule as much as anyone, but it's a good one to keep.

Back to work stuff. Tracking **[cycle time](https://www.lean.org/lexicon-terms/cycle-time)** and **[lead time](https://pm.stackexchange.com/a/15622)** is also helpful because it identifies areas where work in progress can be done more efficiently. The most basic idea is to try to _work on as few issues in parallel as possible_. A colleague recently pointed me to improvement strategies in this area (thanks [Leandro](https://www.linkedin.com/in/leandrolages)), so now I can recommend some resources:

  - 👀 &nbsp; [Avoid the Resource Utilization Trap](https://youtu.be/CostXs2p6r0)
  - 👀 &nbsp; [Multiple WIP articles vs. single-part flow](https://youtu.be/Yqi9Gwt-OEA)
  - 📊 &nbsp; [Google's report on DORA metrics](https://cloud.google.com/blog/products/devops-sre/take-the-2022-state-of-devops-survey) 
    - _Reminder: deployment frequency, lead time, change failure rate, time to restore_
  - 🎧📱📚 &nbsp; [Accelerate: Building Performing Tech Organizations](https://www.amazon.com/Accelerate-Building-Performing-Technology-Organizations/dp/B07BMBYHXL)

It's important to keep in mind that both lead time and cycle time are easy to manipulate (think: small pull requests, dependabot, lint auto-fixes, etc). [KPIs](https://en.wikipedia.org/wiki/Performance_indicator) like these two are only useful if they are not manipulated, so watch out for that.

> When a measure becomes a target, it ceases to be a good measure
>
> <cite>[Goodhart's Law](https://en.wikipedia.org/wiki/Goodhart%27s_law)</cite>

#### 2️⃣ &nbsp; Distributed Backlogs

This might be my favorite. It's about replacing your huge backlog with several small, highly specialized, and highly focused task lists. You're already doing this when you open [20 StackOverflow tabs](https://stackoverflow.blog/2022/07/27/always-learning) while developing a feature, try them all until one works, and then close them all when you find a solution. I apply the same principles in my personal and work life.

In my case, I rely heavily on simple tools and careful scheduling to spread out my backlog, while applying the **zero-inbox policy** all the time, everywhere. I've written about this in other parts of this series, but again, without prioritization, sizing and proper scheduling, you're only addressing the consequences, not the cause.

Here are some examples of what I mean:

  - I use [Chrome Tab Groups](https://blog.google/products/chrome/manage-tabs-with-google-chrome) to organize tasks. I have a **maximum of 3 groups**, at least one of which needs to be active. Remember: limit the WIP items.
  - I treat regular Chrome tabs as work tasks. When a tab is open, I need to do something in it and close it. I can have a **maximum of 10 tabs** open (which is probably a lot). I put the urgent ones on the right, while the rest are sorted by priority from right to left.
  - [Slack reminders](https://slack.com/resources/using-slack/how-to-use-reminders-in-slack), which I also write about in other parts of this series.
  - At work, I like to have a separate tracking board for **Discovery** (things we're researching or preparing) and not pollute the main, Engineering board. That way we have a good overview of upcoming initiatives without polluting the main workspace and backlogs.

There are few things more satisfying than being done with something. 😄  
On a side note, I feel like this way of getting things done boosts my confidence. It definitely helps me deal more calmly with the usual mountain of work that needs to get done.

#### 3️⃣ &nbsp; Remove Ideas from the Backlog

This is only about long-term ideas, not flashes of inspiration that come now and then. The rule is simple: rather than throwing long-term ideas and concepts into the same black hole backlog, I prefer to move them to the [Tech Radar](https://www.thoughtworks.com/radar). The radar can look like this, for example:

{:refdef: style="text-align: center;"}
![Tech Radar](/images/posts/time-management-tech-radar.png)
*A fancy version of a Tech Radar*
{: refdef}

In my personal life, I don't do this. At work, I think it's important to meet with the team from time to time and review the radar. It doesn't have to follow this format, but it should be a list of ideas and suggestions that don't require urgent resolution. Initiatives and ideas that get a high priority (after team discussions) can be moved to the Discovery Board where they'll be studied and prepared for engineering. Rejecting requests is a whole other story, which I write about in the **Prioritization** section of this series.

{:refdef: style="text-align: center;"}
![Solutions](/images/posts/time-management-idea.png)
{: refdef}

-----

## In conclusion…

I make no apologies for the clickbait title, though! If you've been paying attention, it's not that I have anything against the idea of backlogs (per se), but I really don't like the way backlogs are managed in most places and by most people today. 

A lot of people close to me would be surprised by this… but I think it's too much to expect everyone to be as disciplined about these things as I am. I understand that. 😄

So I think it's safer now to tell people that **<font color="#F88">backlogs are evil</font>** and they should just try to **get rid of them**… and others will find good ways to mitigate the problem, which in return might help me organize my backlogs better. You are not the problem, the backlog is! 😄

{:refdef: style="text-align: center;"}
![Thank you](/images/posts/time-management-pray.png)
{: refdef}

-----
