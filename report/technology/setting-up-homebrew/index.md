---
created: 2017-09-23T05:00Z
title: Setting Up Homebrew
type: page
updated: 2018-04-12T00:10Z
---

Any command-line user will know that a robust [package manager](https://en.wikipedia.org/wiki/Package_manager) is not only essential, but something that is a great advantage over your typical GUI. All of the major Linux distributions have package mangers built in: [Arch Linux](https://en.wikipedia.org/wiki/Arch_Linuxn) has [pacman](https://wiki.archlinux.org/index.php/Pacman), [Debian](https://en.wikipedia.org/wiki/Debian)-based distributions have [APT](https://en.wikipedia.org/wiki/APT_(Debian)), [Fedora](https://en.wikipedia.org/wiki/Fedora_(operating_system)) has [rpm](https://en.wikipedia.org/wiki/Rpm_(software)), and [Gentoo](https://en.wikipedia.org/wiki/Gentoo_Linux) has [Portage](https://en.wikipedia.org/wiki/Portage_(software)). But out of the box, there is no package manager for [macOS](https://en.wikipedia.org/wiki/MacOS).

[Homebrew](https://en.wikipedia.org/wiki/Homebrew_(package_management_software)) is a community-created package manager for macOS that functions just like any other package manager for Linux. Applications are simple to install, with simple commands to do so. Dependencies are handled automatically by Homebrew, meaning one only needs to tell it to install the application they want, and all of its requirements will be installed as well. All applications can be updated with a single command. And since this all runs through the terminal, it can be scripted and runs fast compared to updates through the [Mac App Store](https://en.wikipedia.org/wiki/Mac_App_Store).

## Installing Homebrew

### Prerequisites

- macOS 10.10 Yosemite or higher
- [Xcode](https://developer.apple.com/xcode/) or the Command-Line Tools installed

### Installation

Copy and paste the following code into an [iTerm](https://en.wikipedia.org/wiki/ITerm2) or [Terminal.app](https://en.wikipedia.org/wiki/Terminal_(macOS)) session:

	/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

By default, [Homebrew uses Google Analytics](https://github.com/Homebrew/brew/blob/master/docs/Analytics.md) to determine how it is being used. This is used to determine what features are a priority and which applications to include in the package manager. For privacy reasons, analytics can be turned off with the following command.

	brew analytics off

Once Homebrew is installed, the next step is to make sure that it is fully updated with all of the latest applications. To do this, run the following command.

	brew update

With that, Homebrew is installed and fully up-to-date, ready to be used.

## Basic Commands

### install

Installing an application through Homebrew is as simple as typing the following command, replacing <application> with the name of what you want to install:

	brew install <application>

### update

To update Home and all applications within Homebrew, type the following command:

	brew update
 
 This will update the list of installable applications, as well as showing you which of your installed applications have upgrades available.

### upgrade

To upgrade every application managed by Homebrew, run the following command:

	brew upgrade

To upgrade a single application, type its name after the above command:

	brew upgrade <application>

### list

To see a list of everything currently installed by Homebrew, enter this command:

	brew list

### info

Since Homebrew manages dependencies automatically, installing one application can end up installing multiple things at once. To view more detailed information about a particular application, enter the following command:

	brew info <application>

This will provide information about what the application is. It will also include a list of required dependencies for that application, with a notation as to whether it is or is not already installed.

### pin and unpin

To prevent an application from being updated, type the following command:

	brew pin <application>

Once you are ready to allow an application to be updated again, enter the command:

	brew unpin <application>

### cleanup

When applications are upgraded, the previous versions are not removed from the computer. To remove all old versions of applications, enter the command:

	brew cleanup

If you would like to see everything that would be removed along with a total amount of disk space used by these old versions, enter the command:

	brew cleanup -n

In about 4 months of my own heavy Homebrew usage, this meant freeing up around 500 megabytes of storage.

### doctor

If Homebrew acts up, or a new version of Xcode has been installed, Homebrew has its own internal diagnostics command that will find errors within itself and correct them. To do this, enter the following command:

	brew doctor

If Homebrew is unable to fix itself, this command will also output what is wrong and guide you in how to fix the problem.
