---
layout: post
title: Jekyll blogs are still relevant!
description: This is a story about how I run this blog "for free"
date: 2022-12-10 15:00:00 +0100
image: '/images/posts/typewriter-dark.jpg'
tags: [op-ed, blog, writing, tech]
featured: false
---

## History

_[⏭️ Skip to the next section](#up-and-running) if you aren't interested in the backstory._

-----

#### 🧠 &nbsp; Learning about data loss

Back in about 2008, I started "this" blog as a **[Joomla](https://www.joomla.org)** website. Remember [Joomla](https://www.joomla.org)? Heh. Those were good times! 😅  
I hosted it on GoDaddy's basic web hosting, set up Apache, PHP and MySQL myself and configured everything manually. Data transfer was done via FTP ([FileZilla](https://filezilla-project.org)!) and there was no [version control](https://en.wikipedia.org/wiki/Version_control) in place. The blog was black, white and yellow, and named simply: **IT Stuff**!

Moving on -- the year is 2010, and at that time Wordpress became way more popular, so I started migrating my blog to Wordpress. I'm referring to **[Wordpress.org](https://wordpress.org)** -- the self-hosted version I used to run at GoDaddy -- and not [Wordpress.com](https://wordpress.com), the managed/paid version. I don't think "managed" was even an option at the time. 🤔  
Unfortunately, all my blogposts from that time have been lost… because there was a Joomla -> Wordpress migration plugin that I had misconfigured and… well, you know how it is when you don't have version control.

#### 📝 &nbsp; Writing online, made easy

It's now 2014 and Tumblr was recently acquired by Yahoo for $1 billion. Tumblr had a nice user interface for writing content and a modern mobile app with good support for writing on the go. Tech/organizational blogs didn't really exist on Tumblr, but I still felt adventurous and wanted to move there.

Around the same time, Medium was becoming more popular and some of the big tech companies were moving their dev teams there as well. Despite the clean design and ease of use, I never liked it because it was unclear how to migrate… but mostly because I didn't want to support a company that tracked its readers and put up a [paywall in front of](https://qr.ae/pG699l) them without explanation. If you want to make money writing, I'd recommend moving to [Substack](https://substack.com).

But back to my migration to Tumblr! I still hadn't learned from my past mistakes. I tried using another migration plugin to move from Wordpress to Tumblr… 😅  
In my defense, I have to say that this time I had a backup because the old blog was still on GoDaddy. The automatic migration failed (of course) and I finally decided to migrate the posts manually, one by one. This was a good opportunity not only to clean up all the useless nonsense I'd written over the years, but also to redesign and rebrand the blog. Thus, [Angry Byte](https://angrybyte.me) was born! A black and white clean design with a red accent.

#### Ⓜ️ &nbsp; The current iteration

It's 2021 and like it or not, developers and techies love a nice dark theme. I couldn't find a good way to create a good dark theme anywhere else, so I decided to start looking into creating the blog on my own. There are some important reasons why I wanted to host everything myself (once again):

  1. I have more control over the design
  1. I'd rather control what [my DNS](https://www.cloudflare.com/dns) does than leave it to another company
  1. My automation skills are good enough to migrate things with my own code (if needed)
  
With that, I decided to close Angry Byte and move the blog to my own personal domain -- [milos.marinkovic.xyz](https://milos.marinkovic.xyz).

{:refdef: style="text-align: center;"}
![History](/images/posts/jekyll-history.png)
{: refdef}

-----

## Up and running

I had some important requirements for my new blogspace:

  - 💰 &nbsp; Free to host
  - 🎨 &nbsp; Easy to customize
  - 📝 &nbsp; Markdown support
  - 👀 &nbsp; Auto-deploy on every change
  - 🤝 &nbsp; Collaborate with people
  - 🌚 &nbsp; Good dark theme

After a little research, I found that I can simply use the tools we all use every day -- **GitHub**.

#### 📂 &nbsp; GitHub Pages

Enter: [GitHub Pages](https://pages.github.com). They basically give you a folder to put your entire site in, and it's hosted for free at `your-site.github.com`. You get one free site per GitHub account or organization and unlimited project sites. It's as easy as [creating a new Git repository](https://github.com/new), really… so history, version control, reviews, and all that for free.

{:refdef: style="text-align: center;"}
![GitHub Logo](/images/posts/jekyll-github-logo.png)
{: refdef}

##### So, <font color="#F88">what are the downsides</font>?

  1. You can only host **static pages**, i.e. frontends. GitHub doesn't provide a computing service for the backend, nor does it host your databases. You can still find a free backend and a free database, just not through GitHub. I don't need anything other than a front end for my blog.
  1. By default, repositories that can be deployed on GitHub Pages **must be public**. It's also possible to keep them private, but I think you have to pay for that. I don't mind the bulic repository because my blog is public anyway.
  1. You're kind of **tied to Microsoft**. I mean, that's not dramatic either… Git is a distributed storage technology. You can just clone your Git repository to another location and you're free from them. You do have to re-upload your repository to another server in that case, but there's no risk of data loss like with simple FTP or other managed services.

##### What about <font color="#F88">adding</font> and <font color="#F88">editing</font> content? <br> Is there a <font color="#F88">CMS</font> like you know from Medium, Wordpress and other providers?

No, not in that sense. But there's a very good substitute for a CMS with GitHub Pages.

#### 🧪 &nbsp; Jekyll Blogs

GitHub mainly supports [Jekyll](https://jekyllrb.com), among **other** static website generators. I really like how these sites are laid out and how easy they are to manage. To go into a little detail… here's how Jekyll works in a nutshell:

  1. Write the basic HTML layouts (or choose from [hundreds of themes](https://gprivate.com/62b76))
  1. Write your styles in CSS/SASS ([or just choose](https://gprivate.com/62b76))
  1. Write your pages and posts with [Markdown](https://www.markdownguide.org/getting-started)
  1. Start the Jekyll generator engine with `jekyll build`
  1. Take the complete static website generated from that
  1. Upload the generated files to your website hosting

{:refdef: style="text-align: center;"}
![Jekyll Flask](/images/posts/jekyll-flask.png)
{: refdef}

##### But wait! <br> With GitHub Pages <font color="#F88">it's much easier</font>!

All Jekyll website themes are already set up for GitHub Pages and ready to go. Once GitHub detects a Jekyll blog in your repository, it automatically knows what to do! After you select a theme, all you have to do is **add and edit Markdown documents**. And it only takes 5 milliseconds to [get familiar with Markdown](https://www.markdownguide.org/cheat-sheet), even if you've never tried it before.

The only technical knowledge you need to run a simple Jekyll blog is knowing [how to edit files](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll) on the GitHub platform (which is also pretty easy).

#### ⚡️ &nbsp; Where to next?

If this got you interested, you can jump to the [GitHub Pages Quickstart ⤴️](https://docs.github.com/en/pages/quickstart).

My blog's source code (HTML, CSS, Markdown) is also [in a GitHub repository ⤴️](https://github.com/milosmns/milosmns.github.io). Note that my blog's theme is **license-protected** and can't be used without an explicit consent from the author.

And once again, it's **3** steps only: [<font color="#F88">1</font>] choose a theme, [<font color="#F88">2</font>] push the site to GitHub, [<font color="#F88">3</font>] start adding and editing Markdown files! Oh, and yes! Custom domains (such as this one) are also an option -- you can configure domain routing in GitHub repository settings, next to where you enable GitHub Pages.

{:refdef: style="text-align: center;"}
![Jekyll Deployment](/images/posts/jekyll-rocket-deploy.png)
{: refdef}

-----

## Getting technical

This material is for the advanced users. I want to share some tips and tricks about Jekyll and how I manage things locally.

#### 🤔 &nbsp; Why run locally?

If you don't run the blog on your home computer to check, you have to `git commit` every time you make a change, `git push` those changes to GitHub, and finally wait for GitHub to build your site and deploy it to GitHub Pages. This takes forever and is especially annoying if you're making small cosmetic changes. So much time wasted…

#### 🙋‍♂️ &nbsp; Tips & Tricks

GitHub already provides a really **[nice overview here](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)** on how to run the blog on your own machine.

##### An overview of what I do

**<font color="#F88">1</font>** &nbsp; &nbsp; **Save your website to a local directory** on your own computer. You probably already have that if you uploaded your theme to GitHub. If you somehow don't have a local copy but do have a GitHub repository… well, you did something wrong. Now you need to [clone your GitHub repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) to a local directory of your choice.

{:refdef: style="text-align: center;"}
![Blog in Finder](/images/posts/jekyll-directory-disk.png)
*Jekyll blog on my local machine*
{: refdef}

**<font color="#F88">2</font>** &nbsp; &nbsp; **Install the Jekyll engine locally**. Here's a link to some installation requirements and the installation process itself: [Jekyll Installation ⤴️](https://jekyllrb.com/docs/installation/#requirements) -- follow the installation instructions for your operating system.

{:refdef: style="text-align: center;"}
![Jekyll tools installed](/images/posts/jekyll-terminal-tools.png)
*Installation requirements satisfied*
{: refdef}

If you're sure you have everything installed, but still get the "command not found" error for these tools, it may be that your installed tools aren't resolved in your system path. [Look here](https://superuser.com/questions/284342/what-are-path-and-other-environment-variables-and-how-can-i-set-or-use-them) to see what I'm referring to. The most common problem is that Ruby isn't in the Path by default, which [can be easily solved](https://letmegooglethat.com/?q=how+to+add+ruby+to+path) as well. After adding the tools to your Path, restart your command line window to apply the changes.

**<font color="#F88">3</font>** &nbsp; &nbsp; **Make the changes to your website**, whether it's the layout (HTML), the styles (CSS), or the content (Markdown). You can also change the general configuration of the website by editing the `_config.yml` file. All these changes can be tested and verified locally on your computer without publishing anything on GitHub.

It's still a good practice to make commits using Git (with [meaningful commit messages](https://wiki.openstack.org/wiki/GitCommitMessages) to maintain a good change history. And of course, using Git tags is a must - if you're happy with the state of the site, you can just put [a tag](https://linuxhint.com/use-git-tags) there with a meaningful name (like "stable version 1.0"). If you're unhappy with the look of the site, you can [go back in history](https://stackoverflow.com/a/18354193/2102748) by looking up a specific tag. It's very likely that you'll have to use `git push --force` instead of `git push` after going back through history, as the differences between the local and remote states are too large to merge manually.

{:refdef: style="text-align: center;"}
![Git History](/images/posts/jekyll-terminal-git-history.png)
*Git history of my blog*
{: refdef}

**<font color="#F88">4</font>** &nbsp; &nbsp; **Run the generator locally**. Jekyll collects all website resources and then generates the final static website. To do this, run the "build" command:

```bash
jekyll build
```

If there are problems with the configuration or the contents of the website, this command will fail with a clear error message. But a locally built website isn't really useful unless you view it in the browser. For this to work, you have to execute the "serve" command:

```bash
jekyll serve
```

You should then get a link to where your site is currently running, which is usually `http://localhost:4000`.

{:refdef: style="text-align: center;"}
![Jekyll running](/images/posts/jekyll-terminal-running.png)
*Jekyll running locally*
{: refdef}

**<font color="#F88">5</font>** &nbsp; &nbsp; The kicker: if you want to **keep editing your Markdown files** while `serve` is still running, you can instruct Jekyll to automatically update your local website! It's called an "incremental build", and with it enabled, you can just refresh your browser and you can see the changes immediately. Here's how you do it:

```bash
jekyll serve --incremental
```

{:refdef: style="text-align: center;"}
![Jekyll incremental builds](/images/posts/jekyll-terminal-incremental.png)
*Jekyll incrementally changing the website on each change*
{: refdef}

#### 📜 &nbsp; One more thing…

It's easy to forget all these commands, especially if you don't write every day. That's why I have a rule of making a script out of everything that's easy to forget. In my example, I created an executable bash script that runs my website locally (sorry Windows users, it's `.bat` for you).

It's a [really simple](https://github.com/milosmns/milosmns.github.io/blob/master/run.sh) script, it's just easy to forget.

```bash
#!/bin/zsh
clear
jekyll clean
jekyll serve --incremental --host 0.0.0.0 --port 80
open http://localhost
```

Here's what that does:

  1. Clears the command line window
  1. Deletes the previously created website content
  1. Generates the entire website from scratch (`serve` does it first)
  1. Starts watching for content changes (`--incremental`)
  1. Runs Jekyll on the `0.0.0.0` IP address, which is the same as `localhost`
  1. Runs Jekyll on port `80` instead of `4000`. Because port 80 is synonymous with HTTP, I can now go to `http://localhost` without the `:80` suffix
  1. Opens the local blog in my default browser

{:refdef: style="text-align: center;"}
![Jekyll running locally](/images/posts/jekyll-running-locally.png)
*Jekyll blog running locally*
{: refdef}

With this script ready, I [auto-jump](https://github.com/wting/autojump) to my blog directory and run the script. After a couple of moments, my local blog is available in the browser.

```bash
j milosmns  # same as  'cd ~/dev/open/milosmns.github.io/'
./run.sh
```

#### 📣 &nbsp; Spreading the word

A good recommendation for editing Markdown files is [Dillinger.io](https://dillinger.io). It's a free tool that runs in your browser and gives a nice preview of what your Markdown would look like in the finished product.

Otherwise, I also often use [Visual Studio Code](https://code.visualstudio.com) and its GitHub variant -- you know, the one that pops up when you hit `.` on the repository's home page or replace `.com` with `.dev` in your repository's URL. There's a Markdown plugin that works nicely in there.

When you're finally satisfied with the changes, [make a normal message-commit](https://www.atlassian.com/git/tutorials/saving-changes/git-commit) and [push the changes](https://www.atlassian.com/git/tutorials/syncing/git-push) upstream to GitHub, as you would usually do. GitHub will check your changes one last time, generate the new static website, and finally deploy it to `your-site.github.com` or a custom domain (if so configured).

**<font color="#F88">–</font>**

I hope this wasn't too hard! See you on the blog. 👋

{:refdef: style="text-align: center;"}
![My blog](/images/posts/jekyll-blog-icon.png)
{: refdef}
