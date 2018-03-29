---
category: programming
created: 2018.03.29:0230
title: Updating Sublime Text
type: page
updated: 2018.03.29:0230
---

For 7 years, Sublime Text has been my go-to text editor for everything. No other text editor I have used matches the speed of Sublime, and the customization options available rival most other editors out there.

This past year, I decided it was time I spent some significant time with all of the other major text editors out there to see if there was anything I could learn from them. Sublime has treated me well, but many programmers have strong opinions on why they use their editor of choice. I know my reasons for choosing Sublime, but a lot of that came from discounting other editors on spec and not from using them.

Throughout the year, I used the following editors for 2-4 weeks at a time. During this time, I made a list of what I liked and disliked about each editor.

- Emacs
- Neovim
- Atom
- Visual Studio Code
- AppCode & CLion

## Emacs

One half of the classic [editor war](https://en.wikipedia.org/wiki/Editor_war), [Emacs](https://en.wikipedia.org/wiki/Emacs) is still one of the most interesting text editors available. Where it differs from everything else is that it is not merely a text editor: it is a fully interpreted [Lisp](https://en.wikipedia.org/wiki/Lisp_(programming_language)) environment that just happens to have a text editor as its main tool. Despite being created back in the 1970s, Emacs still sees frequent use to this day solely because of this extensibility.

While I have done basic text editing through a terminal before, Emacs is the first full-featured editor that I spent a significant amount of time with. Despite the visuals being basic compared to a standard GUI text editor, the advantages of working inside a terminal environment made up for it. Through the use of [iTerm2](https://en.wikipedia.org/wiki/ITerm2) and [tmux](https://en.wikipedia.org/wiki/Tmux), it's easy to integrate Emacs together with other terminal tools to create an IDE-like environment. One of the biggest advantages to this is that everything can then be done without using a mouse. Switching between terminal panels with the keyboard is incredibly fast, although it does require some memorization of keyboard shortcuts.

I've always been a fan of customizing the tools I use. The most apparent way is through color schemes and custom keyboard shortcuts. By using Emacs together in the same terminal that I use for all of my other tools, I am able to create a unified look for everything. In fact, I can set the terminal to full-screen and not have to see any of the macOS interface. It looks just like a terminal of 30 years ago, but with higher quality font rendering.

When it comes to Emacs itself, the extensibility of the editor can be daunting. First, all configuration is done through [Elisp](https://en.wikipedia.org/wiki/Emacs_Lisp). Unlike the JSON or property names used by most other tools, Emacs requires you to learn a programming language just to configure it. Lisp languages historically differ heavily from non-Lisp languages, so learning Elisp takes some time. One big advantage to this is that the configuration files function more as scripts. If there's weirdness with some plugins, or you just want to transfer your Emacs configuration to a new machine, you simply copy init.el and all supporting files to a clean Emacs installation, and start up Emacs. The configuration script will be run and set everything up as you like, including downloading any plugins used. Since plugins are also written in Elisp, the configuration file has the ability to be as full-featured as any plugin.

The advantage of using Elisp for configuration is that it is more powerful than any other editors plugin system. The disadvantage, and what slowed me down heavily with Emacs, is that it is a lot of information to learn up-front before you can fully take advantage of Emacs. I managed to recreate certain aspects of my Sublime setup in Emacs, but a lot of other things could not quickly be done in the same way.

After my own dabbling with setting up a custom Emacs configuration, I found [Spacemacs](https://en.wikipedia.org/wiki/Spacemacs) and decided to give that a try. Spacemacs is an opinionated distribution of Emacs that includes hundreds of plugins by default, changes the keyboard commands, and structures itself so that support for new programming languages can be easily added without user intervention. The fact that Emacs is an interpreted environment is one of the reasons that it is more resource intensive than other terminal editors like vim, and Spacemacs takes it to an even larger extreme. Even on my 2014 Mac Mini, Spacemacs can take more time to open than Xcode. That said, the functionality that Spacemacs provides is phenomenal, and I plan to spend more time specifically with it just due to how different it functions from stock Emacs.

One of my main resources for Emacs was [Harley Hahn's Emacs Field Guide](http://www.harley.com/emacs/index.html). The first section of Chapter 7 is titled "How to practice using Emacs". This sums up the experience of Emacs as a whole: it is a powerful tool, but it requires practice to use effectively. No other text editor I've used required practice to use just to have the basics down, nor does any other text editor include its own [psychotherapist](https://www.emacswiki.org/emacs/EmacsDoctor) to help you with the existential crises brought about by Emacs.

The lasting impression I have of Emacs is best stated with this quote from Harley Hahn:

> If you want to master Emacs, it helps to believe in reincarnation, because there is no way you are going to learn it all in a single lifetime.

## Neovim

After trying Emacs, the next logical text editor to experiment with is Vim. These two have been pitted against each other for decades, and for good reason. Both editors are exceptional in their way of approaching problems, and drastically different in their approach.

What differentiates Vim from Emacs is that Vim is a modal editor. This means that the editor has an input mode and a command mode, and the user switches back and forth between issuing commands to the editor and inputting text. No other mainstream editor functions this way, although "vim mode" exists for most major editors as an optional plugin.

The specific flavor of Vim that I tried is [Neovim](https://neovim.io), a modern rebuild of Vim programmed with [Rust](https://en.m.wikipedia.org/wiki/Rust_(programming_language)) with a focus on speeding up the Vim architecture. Functionally, Neovim is the same as normal Vim, so the experiences of one would be the same for the other.

As my first modal editor, I loved Vim. Command mode is amazing for editing large portions of the text quickly. Finding specific portions and traversing through the text is quicker than any other editor I have used, including Sublime Text. Since Vim is focused on text editing and not being a heavy programming environment like emacs, it is easier and quicker to jump in and out of Vim without issue. All in all, Vim is a great lightweight editor that still has all of the expandability I expect out of an editor.

Compared to Emacs, Vim is easy to pickup. There are a lot of commands available in Vim, but the basics are similar to how other text editors function. Plugins function similar to how they do in Sublime, so the only learning curve was getting used to modal editing and a different set of keyboard shortcuts. Neovim has some nice defaults compared to normal Vim but both can be used interchangeably right now, although that will likely change in the future as more plugins come out that are specific to neovim.

## Atom

[Atom](https://en.wikipedia.org/wiki/Atom_(text_editor)) is a text editor that I have had a love-hate relationship with ever since its release. In theory, Atom is geared towards someone like me. It's main defining feature is to provide the user complete control over every aspect of the editor, allowing for it to be as heavy or light as the task dictates. Whether that's being a basic text editor or trying to compete with IDEs, Atom's design allows most tasks to be filled.

In this way, Atom succeeds. The plugin ecosystem is rich, customizability of the editor is superior to any other option out there, and due to the web-based nature of its GUI, it can perform tasks that command-line editors can not.

But that web-based GUI is the source of Atom's problems. Atom runs on [Electron](https://en.wikipedia.org/wiki/Electron_(software_framework)), which renders all GUI elements of an application as a webpage. The key advantage of Electron is that it is easy to create cross-platform applications with it. The downside is performance. Atom is slower in almost every way compared to every other editor and IDE that I have used. Even [JetBrain's](https://en.wikipedia.org/wiki/JetBrains) IDEs, which runs on [Java](https://en.wikipedia.org/wiki/Java_(programming_language)), is faster than Atom. Atom is slower to open, introduces significant typing lag, and does not support large files.

My experience with Atom always comes in groups of a few days each. Whenever there is a new release, I try it again for a few small tasks. Despite performance getting better with each update, it still is far from being acceptable for me. It also brings nothing to the table that can't be replicated by IDEs. Since it is heavier than JetBrains IDEs and Xcode, I will opt to use those for IDE tasks.

If GitHub one day fixes all of the performance issues, I would love to give Atom another shot. But until that day comes, it's an editor that I can not use.

## Visual Studio Code

[Visual Studio Code](https://en.wikipedia.org/wiki/Visual_Studio_Code) is an editor that took a while for me to warm up to. It is Electron-based like Atom, which presents some performance issues, but it manages to address the typing lag of Atom, making it an editor I don't mind using. Visual Studio Code proves that Electron does not have to be horrible, although it is not quite as responsive as Sublime.

Code is an interesting editor to use. Due to how Microsoft has designed it, it comes with support for many IDE features right out of the box. The most important of these features centers around Microsoft's [Language Server Protocol](https://en.wikipedia.org/wiki/Language_Server_Protocol), which has the goal of providing an interface for IDE features for any editor. This includes auto-completion, debugging, and refactoring support. Many popular languages already have servers that use this, allowing Code to act as an IDE for these languages without having to wait for an IDE to be created. This is great for newer languages like Rust, where the community can focus on making an implementation for this protocol, and have support for any editor that supports it.

Microsoft continues to put a lot of resources into Code, and the plugin community that has formed around it reminds me of where Sublime's was a few years ago. A lot of languages have both better support in Code than other editors, and that support lands there first. It is an opinionated editor in how it handles files, and seems to mimic Visual Studio in how it functions.

# Taking This All Back to Sublime

Despite not having any plans to go back to most of the editors I experimented with, I did take away something from many of them.

One of my favorite aspects of Emacs and Neovim has to do with the environment you operate them both in. Inside of a command-line, it is easy to create a cohesive color theme so that the entire working environment has the same style. This is harder to replicate in a GUI environment, unless one likes the default white theme of macOS. Since I am not one of those people, I had to settle on either creating my own custom color theme for every application I used, or find one of the rare ones that is universal. One theme that is available for most editors is [Dracula](https://draculatheme.com). In addition to being available for most applications that can be themed, it is a nice dark theme that agrees with my eyes. I now use it for iTerm, Sublime Text, Textual, Xcode, and any other applications that it is available on.

When experimenting with Emacs and Neovim, I used the command-line versions of them and did not enable mouse support. Both editors are known for their quick if not convoluted keyboard shortcut system, and the only way to force me to learn them was to use each editor in an environment where my trackpad is not a viable option. Once I got used to this arrangement, I loved it. Learning the keyboard shortcuts took a lot more work up front, but after a few weeks, most actions were quicker than when I used the trackpad. Learning Sublime's keyboard shortcuts took some time, but now I am able to replicate this workflow easily from the comfort of a GUI. Sublime Text's Command Palette helps where most menu commands and plugin actions can be called from it, so if I forget a shortcut, I can pull it up that one. Unfortunately, this is one area that I can not easily replicate in Xcode. Too many actions in Xcode are reliant on a mouse or trackpad. I have thought of using [AppCode](https://www.jetbrains.com/objc/) solely for this ability, but my dislike for other aspects of AppCode outweighs my desire to be keyboard only.

Up until the last few years, code completion in editors that weren't focused on a single language has been hit and miss. Some languages have decent code completion support(C++, Python), whereas others are non-existent(Swift). One of the big features that Microsoft introduced with Visual Studio Code is their Language Server Protocol. This feature is an interpreter for servers that are focused on providing IDE features for a language. Where this improves on previous implementations is that a programmer only needs to target the Language Server Protocol, and then another plugin handles integration with each editor. All of the major editors have support for these Language Servers now. Instead of having to track down a plugin for each language in each editor, I just have to find the Language Server Protocol plugin, and all of my installed language servers will work automatically. Sublime Text has a strong Language Server Protocol plugin called [LSP](https://github.com/tomv564/LSP), and I now use it whenever I dabble with a language that is not Swift. LSP and the Rust language server instrumental in improving my understanding of the Rust language, as it provides code completion, refactoring, and inline error messages. With the different language servers, I have many of the advantages of an IDE without the bloat and extra features that I do not use.

The big takeaway from using other editors, especially the command-line based ones, is a reinforcing of how much I enjoy the [Unix Philosophy](https://en.wikipedia.org/wiki/Unix_philosophy). No matter the amount of plugins you use, Emacs and Neovim won't have all of the same features as an IDE, but treating the entire command-line environment as an IDE can get you all of those features. Other tasks such as debugging can be accomplished easily with third-party tools. With this in mind, when going back to Sublime, I did not feel a desire to have every IDE feature replicated, just the important ones for directly manipulating code. Other features can be run through a separate command-line, or even another GUI application. For many languages, this provides the perfect environment for how I use the languages. Heavier Swift applications I still relegate to Xcode, but even light Swift scripting is just fine from Sublime and run through the command-line.

# Conclusions

This long exploration of other editors has only reinforced my attachment to Sublime Text. All of the other editors have great features to them, but the cons of them outweigh their advantages. Sublime Text, to me, sits well right in the middle of everything. It has great support for basic IDE features through the use of plugins. It has a myriad of themes that allow it to visually stand with the rest of my environment. It is one of the most performant editors on the market. It's cross-platform, so if I switch to Linux one day, I can take it with me.

The big takeaway from exploring the editors of old is to keep an open-mind in trying new ones. Editors like [xi](https://github.com/google/xi-editor) or GitHub's experimental [Xray](https://github.com/atom/xray) have potential to be good. When they are in a working state, I will be sure to try them out. Sublime Text has been a mainstay of mine for quite some time, but it won't necessarily be there always. Just as it surpassed older editors like [TextMate](https://en.wikipedia.org/wiki/TextMate), so to can other editors surpass Sublime. I don't need to change just for the sake of it, but knowing whats available means I can better choose which editor is best for me.
