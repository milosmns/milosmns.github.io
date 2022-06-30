---
layout: post
title: Preparing a Mac for Engineering work
description: It's a bunch of little things that I do whenever I need to set up my Mac for development or other engineering work
date: 2020-03-23 15:00:00 +0100
image: '/images/posts/work-desk-mac.jpg'
tags: [op-ed, mac, setup]
featured: false
---

#### Motivation

Due to the circumstances that unfolded over the past 3 months, I had to switch and set up my work laptop 4 times. From scratch. It's seriously annoying to go through the same setup every time... and that's why I wanted to be smarter and take notes to remind myself about all the little things I have to repeat during setups. The goal is have the same work environment on each new machine.

This is more of a checklist for me than it is for you, but you're welcome to steal some ideas. I stole many myself. 😬

## Keyboard Setup

Open **System Preferences** and go through every menu and sub-menu, everywhere. You'll see preferences that need changing.

One example of that -- all of my recent devices had a TouchBar. I find it useless and laggy, and I never found myself using the extra buttons. Good old Function keys are great for me. The setting for this is in **System Preferences** → **Keyboard**

{:refdef: style="text-align: center;"}
![Keyboard Settings](/images/posts/mac-setup-keyboard.png)
*My TouchBar, disabled*
{: refdef}

Another example -- I'm very used to Linux/Windows modifier keys (Ctrl, Alt, Super). It has always been just easier to continue with whatever I was used to... especially knowing that Apple isn't forcing their opinion on this -- macOS allows you to easily swap all modifiers, even Caps Lock. It's done through **System Preferences** → **Keyboard** → **Modifier Keys**.

{:refdef: style="text-align: center;"}
![Modifier Keys](/images/posts/mac-setup-modifiers.png)
*My Modifier Keys, swapped*
{: refdef}

This is the moment when I also connect my Magic Keyboard and my MX Master, because the keyboard behavior is per-device and not system-wide.

## Terminal Setup

{:refdef: style="text-align: center;"}
![Mac Terminal](/images/posts/mac-setup-terminal.png)
*The look of my Terminal*
{: refdef}

Let's make things easy first.

#### Homebrew

How would setting up a development environment on a Mac without [Homebrew](https://brew.sh) work? It's the "unofficial Mac package manager". Well, I won't say that it's impossible to maintain such an environment, it's totally doable... but it's definitely super inconvenient.

You should check the project's homepage for the latest installation instructions.  
Here's what I did from my Terminal:

```console
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

That's all. Installing new software is now a breeze using `brew`.

#### Z-Shell

Your Mac probably already has [Z-Shell](https://formulae.brew.sh/formula/zsh) (`zsh`) installed and set as the default shell. Z-Shell provides a better UX and more features than the basic shells.  
You can check with:

```console
$ which $SHELL # should output: /bin/zsh
$ echo $0      # should output: -zsh
```

If it's there, skip to the next section.

If you're not getting `zsh`, you'll need to install and set up Z-Shell manually. Your default is probably Bash (`/bin/bash`). This Shell was the default before macOS Catalina. With the Catalina release, Apple switched to a new default: Z-Shell. You'll anyway still have your basic shells available in case you need them -- `/bin/bash` and `/bin/sh` -- but [here are some reasons](https://github.com/hmml/awesome-zsh) for why `zsh` is better than `bash` and `sh`. 

To install `zsh` using Homebrew:

```console
$ brew install zsh
```

Super simple, right? Homebrew is awesome. [Check out Homebrew's author](https://twitter.com/mxcl/status/608682016205344768) too.

After installing Z-Shell, you need to set it as your default. If you already see Z-Shell in your path (run `which zsh` to check), you can set it as default like so:

```console
$ chsh -s $(which zsh)
```

If it's not available immediately, it's probably stuck in your Homebrew Cellar. Then it's going to be something like this:

```console
$ chsh -s /usr/local/Cellar/zsh/5.8/bin/zsh # might not be 5.8 for you
```

Restart your Terminal to see the change.

## Fast text editing

You might not like editing files in the Terminal. I can take `nano`, but even that is often slow... so, I do it in a standalone app. My favorite **text editor** is [Sublime Text](https://www.sublimetext.com). It's much better than the default TextEdit app you get with your Mac.

Sublime Text also has fancy code coloring, syntax-related completion, plugins... but I really only see it as a text editor that is also capable of displaying code -- and that's how I use it.

Downloading from the official website works, although it's easier to maintain through Homebrew:

```console
$ brew cask install sublime-text
```

Pro tip #1: after installing, open Sublime Text and choose the `Adaptive` theme from the settings.

Pro tip #2: you'll also get a `subl` command-line helper:

```console
$ subl my_file.txt       # opens file
$ subl Documents/project # opens project
```

## Next-gen Terminal tools

Using `grep` and `find` to search for files from the Terminal is fine. Also, using `cd` to enter directories is fine, and `ls` to list the contents is fine. But all of these can start feeling very repetitive if you often go through a deep structure of directories. Same goes for `sed`.

I found some nice utilities built on top of these ideas that are (1) faster, and (2) provide a better UX.

**1. [AutoJump](https://github.com/wting/autojump)**

This one learns from your usage of `cd`, and gives you the ability to jump across directories with only a few characters typed.

Here's an example of what you can do with AutoJump:

```console
$ pwd
/Users/m.marinkovic

$ j open
Jumped to 'open-source'

$ pwd
/Users/m.marinkovic/dev/open-source
```

It can also guess correctly even with simpler and shorter jump directions, like this one:

```console
$ pwd
/Users/m.marinkovic

$ j a
Jumped to 'android'

$ pwd
/Users/m.marinkovic/dev/android
```

**2. [RipGrep](https://github.com/BurntSushi/ripgrep)**

This one provides really fast text search. Like, reeeeally fast.

{:refdef: style="text-align: center;"}
![RipGrep](/images/posts/mac-setup-ripgrep.png)
*Usage of **rg** in a directory*
{: refdef}

In my case, it takes around 100ms to search any text through all of my projects (27 projects, including the `.git` directories).

**3. [Tree](http://mama.indstate.edu/users/ice/tree)**

This one is used for displaying deep directories in the Terminal.

```console
$ tree .how-to
.how-to
├── assets
│   ├── css
│   │   └── style.css
│   └── img
│       ├── analytics.png
│       ├── config.png
│       ├── disqus.png
│       ├── page.png
│       └── post.png
├── index.html
└── styleguide.md

3 directories, 8 files
```

**4. [FD](https://github.com/sharkdp/fd#on-macos)**

While `find` works fine, `fd` is a simple, fast and user-friendly alternative to it. While it does not aim to support all of `find`'s powerful functionality, it provides sensible (and opinionated) defaults for the majority of use cases.

```console
$ fd mac

_posts/op-ed/2020-03-23-Preparing-Mac-Engineering.md
images/posts/keyboard-mac.png
images/posts/mac-setup-iterm.png
images/posts/mac-setup-keyboard.png
images/posts/mac-setup-modifiers.png
images/posts/mac-setup-ripgrep.png
images/posts/mac-setup-terminal.png
images/posts/work-desk-mac.jpg
```

**5. [SD](https://github.com/chmln/sd#macos)**

Unix' default [`sed`](https://www.gnu.org/software/sed/manual/sed.html) (stream editor) is... well, let's just say that nobody likes to use it. 😝

So, `sd` is the arguably better alternative. It's more intuitive and has different defaults.

Removing chars and whitespace looks like this:

```console
$ echo '"lots((([]))) of special chars"' | sd -s '((([])))' ''
"lots of special chars"

$ echo '"lorem ipsum 23   "' | sd '\s+$' ''
"lorem ipsum 23"
```

Replacing text in file and in project looks like this:
```console
$ sd 'window.fetch' 'fetch' http.js
Replaced in http.js

$ sd 'from "react"' 'from "preact"' $(fd --type file)
Replaced in project
```

## The Terminal

This is the main dish, it's about iTerm, the 'Terminal on steroids' that does everything that your standard Terminal does, plus a [bunch of other useful things](https://www.iterm2.com/features.html) you never knew you needed. It won't make you a 10x developer, but will surely make you feel like one.

It's super easy to install using Homebrew:

```console
$ brew cask install iterm2
```

Once installed, you should immediately open iTerm's settings and reconfigure the defaults. For example, choose the `Minimal` theme.

{:refdef: style="text-align: center;"}
![iTerm Theme](/images/posts/mac-setup-iterm.png)
*iTerm's theming settings*
{: refdef}

You can also specify a directory where to keep your iTerm settings, in case you need to migrate everything to a new machine later.

If you want a fancy color scheme (and you do), check out [this page](https://iterm2colorschemes.com) -- it has a lot of different configuration schemes. Check the installation instructions on top.

## Z-Shell plugins

#### Oh My Z-Shell

This is, arguably, the most interesting part of the process. It's a cosmetical change, sure, but it makes things so much cleaner and easier to navigate through. It's all about picking the right `zsh` theme with a few great plugins. My favorite Z-Shell framework is `OhMyZsh`, but there are other options like `Prezto` and others.

[OhMyZsh](https://github.com/ohmyzsh/ohmyzsh#basic-installation) is a `zsh` framework that makes you feel like your doing something important. No joke. It also supports a bunch of plugins that could boost your productivity (or at least help with readability) and lots of great themes.

To install OhMyZsh, I ran this:

```console
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

You might need to restart your Terminal for the changes to take effect.

#### PowerLevel 10k

I like the [powerlevel10k](https://github.com/romkatv/powerlevel10k#oh-my-zsh) theme on top of OhMyZsh, it's configurable and has support for a bunch of dev tools. Their `git` support is awesome, for example.

To install `powerlevel10k` on top of OhMyZsh, I ran this:

```console
$ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

This command installs the theme, but you still need to specify that you want to use it. You need to **change** the `ZSH_THEME` variable value to `"powerlevel10k/powerlevel10k"` inside of your home directory's `.zshrc`.

Restart your Terminal after. Follow the on-screen instructions once you open it again.

#### Additional plugins

You can see a bunch of other plugins for OhMyZsh [here](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins). I set my favorites in the same `~/.zshrc` file, just find the `plugins` line:

```bash
plugins=(git colored-man-pages colorize pip python macos docker kubectl)
```

## Java Virtual Machines

I usually need a JVM environment. You may be aware of the Java licensing change... basically, Oracle [changed their Java license](https://medium.com/@javachampions/java-is-still-free-2-0-0-6b9aa8d6d244), so their JDK and JRE are not commercially usable anymore. Not for free, anyway...  
**Update**: it seems like they changed back to free licensing. But no thanks.

The "open" version of Java is still free, and can be installed through Homebrew from [AdoptOpenJDK](https://github.com/AdoptOpenJDK/homebrew-openjdk#other-versions), for example.

I ran this:

```console
$ brew tap AdoptOpenJDK/openjdk
$ brew cask install adoptopenjdk8-openj9-jre-large
```

## Environment Variables

To be future-proof, and to make sure that all of my Java programs run with the same (default) JVM version, I specify the `JAVA_HOME` variable in my `.zshrc`. There are also some other things I configure in that file, like `ANDROID_HOME`, which is useful for automated processes and testing CI pipelines. Android SDK comes bundled with your Android Studio installation, and you can point to that one.

Here's a snippet from my `.zshrc` config that sets up Java and Android, and also updates the global `PATH` to include all of the tools.

```bash
# Custom Locations
LOCAL_LINKS_HOME=$HOME/bin:/usr/local/bin
SCRIPTS_HOME=$HOME/Scripts
export JAVA_HOME=/Library/Java/JavaVirtualMachines/adoptopenjdk-8-openj9.jdk/Contents/Home
export ANDROID_HOME=$HOME/Library/Android/sdk
export GRADLE_HOME=/usr/local/Cellar/gradle/5.6.4

# Here's a multi-line PATH hack!
export PATH=$ANDROID_HOME/platform-tools:$PATH
export PATH=$ANDROID_HOME/tools:$PATH
export PATH=$JAVA_HOME/bin:$PATH
export PATH=$SCRIPTS_HOME:$PATH
export PATH=$LOCAL_LINKS:$PATH
```

Did I mention you can also install a local distribution of Gradle (`brew install gradle`)?

## IDEs

To manage my IDEs, I use [JetBrains Toolbox](https://www.jetbrains.com/toolbox-app) with [sync settings to remote repo](https://www.jetbrains.com/help/idea/sharing-your-ide-settings.html#IDE_settings_sync) feature turned on. You can store settings in a private GitHub repository, for example.

My other tools are automatically updated anyway, so no need to worry about them.

## Tips and Tools

What else do you need?

#### Pro tips

- Check for discounts at [Humble Bundle](https://www.humblebundle.com) and [Stack Social](https://stacksocial.com)
- Migrating your scripts? I use `~/Scripts` to store all of mine, this way I can backup and restore easily using a single Git repository
- Migrating XCode configuration? It's in `~/Library/Developer/Xcode/UserData`, including key mappings and color configurations

#### Productivity tools

- Better Spotlight? It's a must-have, try [Raycast](https://www.raycast.com/)
- A better Calendar app? [Fantastical 2](https://flexibits.com/fantastical)
- A better Email client? [Air Mail](https://airmailapp.com) -- another no-brainer
- An open-source, cross-platform password manager? [BitWarden](https://bitwarden.com)
- Your MenuBar is too busy? Hide the clutter with [Vanilla](https://matthewpalmer.net/vanilla) (paid) or [Hidden Bar](https://github.com/dwarvesf/hidden) (free)
- Clipboard manager? [Copy Clip](https://fiplab.com/apps/copyclip-for-mac) works perfectly, it's a **must have**
- All-in-one messenger? [Rambox](https://rambox.app) or [Franz](https://meetfranz.com)
- You miss your split-window feature from Windows? No problem, [Magnet](https://apps.apple.com/de/app/magnet/id441258766?l=en&mt=12)'s got you covered
- Customizable app switcher? [Command-Tab Plus](https://noteifyapp.com/command-tab-plus) is great, includes window switching and allows command remapping
- ~~Tracking your time? Clockify. It has a Mac app and it's easy to use~~  
**NO. NEVER SAY YES TO TIME TRACKING.**

#### Graphics tools

- A great screenshot tool? [Shottr](https://shottr.cc) or [Lightshot](https://app.prntscr.com)
- Vector graphics editor? [Affinity Designer](https://affinity.serif.com/en-us) (paid), or [BoxySVG](https://boxy-svg.com) (paid). [Inkscape](https://inkscape.org) is free but not great
- Raster graphics editor? [Affinity Photo](https://affinity.serif.com/en-us) (paid), [GIMP](https://www.gimp.org) (free) or [Seashore](https://apps.apple.com/de/app/seashore/id1448648921?l=en&mt=12) (free)
- Desktop publishing software? [Affinity Publisher](https://affinity.serif.com/en-us) (paid)
- A professional PDF viewer & editor? [PDF Expert](https://pdfexpert.com)

#### Privacy tools

- A fast, reliable, privacy-oriented VPN? [Nord VPN](https://nordvpn.com) is my choice
- Monitoring your camera and microphone? [Micro Snitch](https://www.obdev.at/products/microsnitch/index.html). They have amazing support!

#### Utilities

- Monitoring your Mac's hardware? [iStatMenus](https://bjango.com/mac/istatmenus) integrates pretty well
- [Service Station](https://apps.apple.com/de/app/service-station/id1503136033?mt=12) allows you to extend Finder's capabilities (Open with..., custom scripts, etc.)
- [New File Menu](https://apps.apple.com/de/app/new-file-menu/id1064959555?mt=12), if you're missing your Windows' "new file" menu
- Your company policy puts your Mac to sleep after 2 minutes? Use [Caffeine](http://lightheadsw.com/caffeine) to keep it awake
- Saving your audio books for later? [Open Audible](https://openaudible.org)

#### Development tools

- [Screen Copier (scrcpy)](https://github.com/Genymobile/scrcpy#macos) will mirror your connected Android devices on the desktop, for free
- [Android Tool for Mac](https://github.com/mortenjust/androidtool-mac#download) allows you to save screenshots, screen recordings and GIFs of your connected Android devices
- A professional, advanced IDE for iOS and macOS development?  
**Sorry, you're stuck XCode** 😬

#### Other

If you know other interesting products, shoot them to [my Twitter](https://twitter.com/milosmns). I can add them here.
