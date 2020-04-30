---
category: automation
created: 2018-10-17T00:30Z
title: Why Automate?
type: page
updated: 2018-10-31T16:00Z
---

Automation is a task that computers excel at. The whole process of a modern computer is automated: press the power button, and a gargantuan list of processes are automatically run just to turn on the machine. Once running, software [daemons](https://en.wikipedia.org/wiki/Daemon_(computing)) are making sure the system remains functional, providing background services for every application running on top of the operating system, and notifying you whenever something is set to do so.

A lot of this automation is built in to the systems we use every day. Most of it is not easily modifyable, but the tools that computers use for their own automation can be leveraged by us for our own purposes. The straightforward example is allowing e-mail clients to notify us when a new e-mail is received, or to turn off and on the lights in our homes at specific times. Knowing how to take advantage of this automation can free up our time to focus on other issues in life.

## Automation Through The Command-Line

One of the reasons I remain a heavy command-line user is due to the ease of automation provided by it. One command can call another, which can send its output to the original command. This allows in-depth chaining of commands that can pull in other external tools, simplifying the task at hand. Common scripting languages are high level, simplifying the creation of scripts that can automate larger workloads. These scripts can then be run manually as needed, or set on an automatic schedule. Unix-like operating systems promote this type of usage by putting the command-line front and center to the user.

There are many ways to automate through the command-line. The basic way supported by all operating systems with a command-line is to use the built-in scripting functionality provied by default. Most commonly this is using [bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)). But other high-level programming languages work great for comand-line scripting. The following are some of them:

- [Julia](https://julialang.org/)
- [Lua](https://www.lua.org/)
- [Perl](https://www.perl.org/)
- [Python](https://www.python.org/)
- [Ruby](https://www.ruby-lang.org)
- [Swift](https://swift.org/)

## Automation With GUIs

Command-line commands are my particular tool of choice for automation when possible, but it is not the only option. Many GUI applications provide forms of automation that are appropriate for the task. There is not a unified system for automation as there is for the command-line, but there is often better support with other graphical portions of the operating system. The visual nature of the application also allows different forms of output than the textual nature of the command-line.

The automation of these applications tends to fall along the lines of running specific tasks under specifc circumstances or at set intervals. Backup programs that run every hour and/or every night; e-mail clients that regularly check for new messages and notify when they arrive; calendars that remind us when to leave for an upcoming event. These are all examples applications built into most common operating systems, with automation providing core functionality to how they operate.

Other examples of graphical automation is in applications like [Photoshop](https://en.wikipedia.org/wiki/Adobe_Photoshop) that provide [batch file processing](https://helpx.adobe.com/photoshop/using/processing-batch-files.html). With this, a directory full of images can have the same edits applied to it, and then have the output saved. All it takes is creating a single version of the output, and Photoshop will repeat it for all other images provided. [ImageOptim](https://imageoptim.com) applies a battery of different compression methods to its provided images, and chooses the best one before providing the final output. This is done seemlessly to the user, cutting down the time to complete its task into seconds instead of the minutes or hours it would take to manually accomplish the same thing.

## How I Automate

The simplest way to automate is to pick a task and research the ways that it can be automated. When looking into automating something new, I keep a few things in mind when deciding what tool would be best for the job.

- Integration with current automation
- Maintenance
- Amount of time to implement
- Price

One advantage of using the command-line as I do is that it provides an easy window into what tasks can be automated. Command-line commands can be long and obtuse. This is especially true for tools that provide dozens or even hundreds of possible arguments, such as ffmpeg. It is often easier to understand how the tool works and create a script on top of it. Abstracting away the information into something automatic and simple is a great way to make using that tool easier.

<https://imgs.xkcd.com/comics/is_it_worth_the_time_2x.png>

Knowing what to automate is the key to saving time. Tasks that are not frequently run will not benefit from automation as much as automating those tasks that are run every day. I personally keep a running list of tasks that I would like to automate, sorted by a mixture of frequency used and time consumed by the task.
