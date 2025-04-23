---
layout: post
title: Preparing a Mac for Engineering work
description: It's a bunch of little things that I do whenever I need to set up my Mac for development or other engineering work
date: 2020-03-23 15:00:00 +0100
image: '/images/posts/work-desk-mac.jpg'
tags: [op-ed, mac, software, setup]
featured: false
---

#### Why this?

Due to the circumstances that unfolded over the past 3 months, I had to replace and set up my work laptop 4 times… from scratch. It's seriously annoying to go through the same setup every time, and it's easy to forget a lot of setup steps. That's why I wanted to be smart and take notes to remind myself about all the little things I have to repeat during setups. The goal is to have the same work environment on each new machine.

This post is exactly that – a checklist for me, but also a buide for you – and you're welcome to steal some of these ideas (I stole many myself). 😬

## Keyboard Setup

Open **System Preferences** and go through every menu and sub-menu, everywhere. You'll see preferences that need changing.

One example of that – all of my recent devices unfortunately had an Apple TouchBar. I find it useless and laggy, and I never found myself using the extra buttons. Good old Function keys are great for me. The setting for this is in **System Preferences** → **Keyboard** → **Keyboard Shortcuts** → **Function Keys**.

{:refdef: style="text-align: center;"}
![Keyboard Settings](/images/posts/mac-setup-keyboard.png)
*My TouchBar, disabled*
{: refdef}

Another example – I'm very used to Linux/Windows modifier keys (Ctrl, Alt, "Super"). It has always been just easier to continue with that, especially now that Apple isn't forcing their vision around keyboard preferences anymore. Latest macOS allows you to easily swap all modifiers, even Caps Lock and the Function key. This is done through **System Preferences** → **Keyboard** → **Keyboard Shortcuts** → **Modifier Keys**.

{:refdef: style="text-align: center;"}
![Modifier Keys](/images/posts/mac-setup-modifiers.png)
*My Modifier Keys, swapped*
{: refdef}

This is the moment when I also connect my [Magic Keyboard](https://www.apple.com/shop/product/MXK83LL/A/magic-keyboard-with-touch-id-and-numeric-keypad-for-mac-models-with-apple-silicon-usb-c-us-english-black-keys) and my [MX Master mouse](https://www.logitech.com/en-eu/shop/p/mx-master-3s-mac-bluetooth-mouse.910-006571), because the keyboard and mouse settings are per-device and not system-wide.

## Terminal Setup

{:refdef: style="text-align: center;"}
![Mac Terminal](/images/posts/mac-setup-terminal.png)
*The look of my Terminal*
{: refdef}

Let's make things easy first.

#### Homebrew

How would setting up a development environment on a Mac without [Homebrew](https://brew.sh) work?? It's the "unofficial Mac package manager", and without it, managing your installations becomes super inconvenient.

You should check the project's homepage for the latest installation instructions.
Here's what I did from my Terminal:

```console
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

That's all. Installing new software is now a breeze, simply using `brew install x`.

#### Z-Shell

Your Mac probably already has [Z-Shell](https://formulae.brew.sh/formula/zsh) (`zsh`) installed and set as the default shell. Z-Shell provides a better UX and more features than the basic Bash shells.

You can check this using:

```console
$ which $SHELL # should output: /bin/zsh
$ echo $0      # should output: -zsh
```

If it's there, skip to the next section.

If you're not getting `zsh` there, you'll probably want to install and set up Z-Shell now. Your default is probably Bash (`/bin/bash`). This Shell was the default before MacOS Catalina. With the Catalina release, Apple switched to a new default: Z-Shell. You'll anyway still have your basic shells available in case you need them – `/bin/bash` and `/bin/sh` – but [here are some reasons](https://github.com/hmml/awesome-zsh) for why `zsh` is better than `bash` and `sh`.

Convinced yet? Good! Now, to install `zsh` using Homebrew:

```console
$ brew install zsh
```

Super simple, right? Homebrew is awesome. [Check out Homebrew's author](https://twitter.com/mxcl/status/608682016205344768) on socials too.

After installing Z-Shell, you can set it as your default shell. If you already see Z-Shell in your path (run `which zsh` to check), you can set it as default like so:

```console
$ chsh -s $(which zsh)
```

If it's not available immediately, it's probably stuck in your Homebrew Cellar. Then it's going to be something like this:

```console
$ # This might not be 5.8 for you
$ chsh -s /usr/local/Cellar/zsh/5.8/bin/zsh 
```

Restart your Terminal to see the changes.

## Fast text editing

You might not like editing files in the Terminal. I can take `nano`, but even that is often slow… so, I usually do it using a fast desktop app. My favorite **text editor** is [Sublime Text](https://www.sublimetext.com). It's much better than the default TextEdit app you get with your Mac.

Sublime Text also has code coloring when editing code, syntax-related completion, plugins… but I really only see it as a text editor that is also capable of displaying code – and that's how I use it.

Downloading from the official website works, although it's easier to maintain through Homebrew:

```console
$ brew install --cask sublime-text
```

Pro tip #1: after installing, open Sublime Text and choose the `Adaptive` theme from the settings.

Pro tip #2: you'll also get a `subl` command-line helper:

```console
$ # How to open a file
$ subl my_file.txt

$ # How to open a project directory
$ subl Documents/project
```

## Better Terminal tools

Using `grep` and `find` to search for files from the Terminal is totally fine. Also, using `cd` to enter directories is fine, and `ls` to list the contents is fine. The same goes for `sed`. But all of these can start feeling very repetitive if you often go through a deep structure of directories, and they lack features for when you need to perform advanced data manipulation.

I found some nice utilities built on top of these core ideas that are (1) faster, and (2) provide a better user experience.

**1. [AutoJump](https://github.com/wting/autojump)**

This one learns from your usage of `cd`, and gives you the ability to jump across directories with only a few characters typed. We use `j` to jump.

Here's an example of what you can do with AutoJump:

```console
$ pwd
/Users/milosmns

$ j open
Jumped to 'open-source'

$ pwd
/Users/milosmns/dev/open-source
```

It can also guess correctly even with simpler and shorter jump directions, like this one:

```console
$ pwd
/Users/milosmns

$ j a
Jumped to 'android'

$ pwd
/Users/milosmns/dev/android
```

**2. [RipGrep](https://github.com/BurntSushi/ripgrep)**

This tool provides really fast text search. Like, reeeeally fast.

{:refdef: style="text-align: center;"}
![RipGrep](/images/posts/mac-setup-ripgrep.png)
*Usage of **rg** in a directory*
{: refdef}

In my case, it takes around 100ms to search any text through all of my projects (27 project directories, including the `.git` directories).

**3. [Tree](http://mama.indstate.edu/users/ice/tree)**

This tool is used for displaying deep directory structures, nicely, in the Terminal.

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

While `find` works fine, `fd` is a simple, fast and user-friendly alternative to it. It doesn't aim to support all of `find`'s functionality 1:1, but it provides sensible (and opinionated) defaults for the majority of use cases.

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

$ fd --extension txt --exclude LG-WebOS-CLI

ZeBadge/zeapp/server/src/main/resources/names.txt
aimages/requirements.txt
appifyhub/charts/secrets-check/templates/NOTES.txt
code-stats/src/commonMain/resources/web/info.txt
demo.github.io/robots.txt
```

**5. [SD](https://github.com/chmln/sd#macos)**

Unix's default [`sed`](https://www.gnu.org/software/sed/manual/sed.html) (stream editor) is… well… people sometimes complain about its usability. 😝 And this tool, `sd`, is an arguably better alternative. It's more intuitive and has better defaults.

Removing chars and whitespace looks like this:

```console
$ echo '"lots((([]))) of special chars"' | sd -s '((([])))' ''
"lots of special chars"

$ echo '"lorem ipsum 23   "' | sd '\s+$' ''
"lorem ipsum 23"
```

Replacing text in a file or in a project looks like this:

```console
$ sd 'window.fetch' 'fetch' http.js
Replaced in http.js

$ sd 'from "react"' 'from "preact"' $(fd --type file)
Replaced in all files
```

**6. [K9S](https://k9scli.io)**

Do you interact with Kubernetes clusters? Kubernetes interaction using `kubectl` can be quite verbose, and `k9s` aims to make it easy, intuitive and usable. Once you enter the `k9s` dashboard, your Terminal becomes a modern graphical user interface!

{:refdef: style="text-align: center;"}
![K9S](/images/posts/k9s-screenshot.png)
*The **k9s** dashboard*
{: refdef}

## The Terminal

Terminal is the main dish of this guide! It's about [iTerm](https://iterm2.com), the 'Terminal on steroids' that does everything that your standard Terminal does, plus a [bunch of other useful things](https://www.iterm2.com/features.html) you never knew you needed. It won't make you a 10x developer, but will surely make you feel like one.

It's super easy to install using Homebrew:

```console
$ brew install --cask iterm2
```

Once installed, you should immediately open iTerm's settings and reconfigure the defaults. For example, the best theme is not selected by default, and it's called `Minimal`.

{:refdef: style="text-align: center;"}
![iTerm Theme](/images/posts/mac-setup-iterm.png)
*iTerm's theme settings*
{: refdef}

You can also specify a directory where to keep your iTerm settings, in case you need to migrate everything to a new machine later.

If you want a fancy color scheme (yes – you do), check out [this page](https://iterm2colorschemes.com). It has a lot of different configuration and schemes that you can directly import.

## Z-Shell plugins

#### Oh My ZSH

This is, arguably, the most interesting part of the setup. Even though it's only a cosmetic change, [OhMyZsh](https://github.com/ohmyzsh/ohmyzsh) makes things so much cleaner and better-looking. Now it's all about picking the right `zsh` theme with a few great plugins. My favorite Z-Shell framework is `OhMyZsh`, but there are other options like `Prezto`, or others.

[OhMyZsh](https://github.com/ohmyzsh/ohmyzsh#basic-installation) is a `zsh` framework that makes you feel like your doing something important. No joke. It also supports a bunch of plugins that help your productivity (or at least help with readability), as well as lots of great themes.

To install `oh-my-zsh`, follow the installation instructions from their landing page. I ran this:

```console
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

You might need to restart your Terminal for the changes to take effect.

#### PowerLevel 10k

I like the [powerlevel10k](https://github.com/romkatv/powerlevel10k#oh-my-zsh) theme on top of OhMyZsh, as it's nicely configurable and has support for a bunch of dev tools. Their `git` support is awesome, for example.

To install `powerlevel10k` on top of OhMyZsh, I ran this:

```console
$ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

This command pulls the theme, but you still need to specify that you want to use it. You need to **change** the `ZSH_THEME` variable value to `"powerlevel10k/powerlevel10k"` inside of your home directory's `.zshrc` or `.zprofile`.

```console
$ # Edit your shell configuration
$ subl ~/.zshrc
```

Restart your Terminal after this change. Follow the on-screen instructions once you open it again to set up your new theme.

#### Additional plugins

You can see a bunch of other plugins for OhMyZsh [here](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins). I set my favorites in the same `~/.zshrc` file, just find the `plugins` line:

```bash
plugins=(git colored-man-pages colorize pip python macos docker kubectl)
```

## Java Virtual Machines

I usually need a JVM environment to run apps and services.

~~You may be aware of the Java licensing change… basically, Oracle [changed their Java license](https://medium.com/@javachampions/java-is-still-free-2-0-0-6b9aa8d6d244), so their JDK and JRE are not commercially usable anymore. Not for free, anyway…~~

**Update**: It seems like they changed back to a free license after a while!

Regardless of the license issues, the "open" version of Java is still free for any type of use, and can be installed through Homebrew from the [AdoptOpenJDK](https://github.com/AdoptOpenJDK/homebrew-openjdk#other-versions) repository, for example.

To get it, I ran this:

```console
$ brew tap AdoptOpenJDK/openjdk
$ brew install --cask adoptopenjdk8-openj9-jre-large
```

## Environment Variables

To be future-proof, and to make sure that all of my Java programs run with the same (default) JVM version, I specify the `JAVA_HOME` variable in my `~/.zshrc` file. There are also some other things I configure in that file, like `ANDROID_HOME`, which is useful for automated processes and testing CI, as well as Android Studio's configuration. Android SDK now comes bundled with your Android Studio installation, so you can simply point to that directory.

Here's a trimmed snippet from my `.zshrc` config that sets up Java and the Android SDK, but also updates the global `PATH` to include all of the tools I need.

```bash
# Custom locations
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

Oh, `GRADLE_HOME`? Did I mention that you can also install a local distribution of Gradle using `brew install gradle`? All your Gradle-based projects can start using the same Gradle version!

## Code Editors

To manage my main IDEs, I use the [JetBrains Toolbox](https://www.jetbrains.com/toolbox-app) with [sync settings to remote repo](https://www.jetbrains.com/help/idea/sharing-your-ide-settings.html#IDE_settings_sync) feature turned on. You can store your settings in a private GitHub repository, for example.

My other tools and code editors are automatically updated and synchronized, so no need to worry about them.

### Other tips

- Check for discounts at [Humble Bundle](https://www.humblebundle.com) and [Stack Social](https://stacksocial.com)
- Migrating your scripts? I use a dedicated `~/Scripts` directory to store all of my scripts – way I can backup and restore easily
- Migrating XCode configurations? It's currently stored in `~/Library/Developer/Xcode/UserData`, including the key mappings and color configurations

I recommend to also check out my [Curated list of Mac tools](/2020/03/22/Mac-Curated-List) for other ideas!
