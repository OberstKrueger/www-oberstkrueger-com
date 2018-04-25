---
category: programming
created: 2017.08.26:1615
title: Scripting With Swift
type: page
updated: 2018.04.25:0205
---

One of the strengths of any [Unix](https://en.wikipedia.org/wiki/Unix)-based operating system is the ability to automate it using custom scripts. A typical script is created using [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) or [Python](https://en.wikipedia.org/wiki/Python_(programming_language)) and run through the terminal or automated using something like [systemd](https://en.wikipedia.org/wiki/Systemd) or [launchd](https://en.wikipedia.org/wiki/Launchd).

Since it's release, one of the interesting prospects of [Swift](https://en.wikipedia.org/wiki/Swift_(programming_language)) has been its use as a scripting language. While Swift is a lower-level language than Python, it's tight integration with [macOS APIs](https://developer.apple.com/documentation/) allow it to be used to fill this purpose. Simplifying matters is the fact that Swift includes a [REPL](https://en.wikipedia.org/wiki/Read–eval–print_loop), allowing Swift files to be passed in and ran without the need to compile them before running. This allows for faster development and testing of any Swift scripts, and makes it possible to run them without worrying whether they are compiled for the architecture they will be running on.

The first step to creating a Swift script is the same as a script in any other language: create an empty text file that has run priviledges.

Just like in a Bash script, the first line of the script will be a [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) pointing the script to the Swift REPL. Bash scripts typically start with *#!/bin/sh*, but for Swift, this will look like *#!/usr/bin/swift*.

After the shebang, any valid Swift code can be executed.

Swift scripts are not limited to the [Swift standard library](https://developer.apple.com/documentation/swift). All of Apple's provided frameworks can be imported without issue. [Foundation](https://developer.apple.com/documentation/foundation) is the most commonly used framework in all of my scripts, but others can be used to interact with different classes of data, such as [Contacts](https://developer.apple.com/documentation/contacts) for editing and retrieving information stored in Contacts.app and [EventKit](https://developer.apple.com/documentation/eventkit) for calendar interactions. Foundation also provides [AppleScript](https://developer.apple.com/library/content/documentation/AppleScript/Conceptual/AppleScriptX/AppleScriptX.html) interactions, allowing scripts to communicate back and forth with applications that are currently running.

An important part of creating scripts is being able to pass commands back to Bash. Python provides a simple function for this, but Swift does not have a simple built-in function. Creating one of my own was simple. Using the [Process](https://developer.apple.com/documentation/foundation/process) class of Foundation provides the commands necessary to create a simple function to pass commands back to Bash. It consists of the following code:

	func runCommand(command: String, wait: Bool = true) {
		let cli = Process()
		cli.launchPath = "/bin/bash"
		cli.arguments = ["-c", command]
		cli.launch()
		if wait {
			cli.waitUntilExit()
			if cli.terminationStatus != 0 {
				print("Error: \(cli.terminationReason)")
			}
		}
	}

The *command* value is a string that contains the Bash command to be passed, and *wait* is a flag to determine whether the script should stop and wait for the Bash command to complete. An example of this function's use is below.

## Test Script - Converting PNGs To JPGs Using Mozjpeg

The first script that I wanted to convert is a simple Python script that converts [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) images to [JPEG](https://en.wikipedia.org/wiki/JPEG) images optimized for web usage using the [Mozjpeg](https://github.com/mozilla/mozjpeg) encoder. This is a common script I use for web development, as the Mozjpeg encoder is one of the most efficient about there.

Mozjpeg does not contain a general purpose image decoder. If you are passing anything other than a JPEG to it, the image will need to first be prepared by another tool. [ImageMagick](https://en.m.wikipedia.org/wiki/ImageMagick) is capable of decoding most image formats available and can convert an image into an intermediary format that Mozjpeg will understand. This two-step process of converting to an intermediary format and then encoding to JPEG is a perfect candidate for scripting, as the full Bash command for the conversion is long:

	convert image.png pnm:- | mozcjpeg -quality 85 > image.jpg

My original script in Python looks like this.

	#!/usr/bin/env python3
	
	from sys import argv
	from os import system
	
	for arg in argv[1:]:
		new_file_name = "{}jpg".format(arg[:-3])
		command = "convert \"{}\" pnm:- | mozcjpeg -quality 85 > \"{}\"".format(arg, new_file_name)
		system(command)

This script makes for a good test case for Swift for a few reasons. First, it is a simple script with minimal logic used. Second, it does not interact with files directly, instead reading input from passed arguments and then passing a command back to the terminal to be run by it. Like with Python, interacting with files directly is possible with Swift, but given that most of my current scripts interact using Bash commands, I wanted to stick with that first.

A new piece needed to complete the script is to accept arguments from the command-line when the script is run. This was easier to figure out than passing commands, as the Swift Standard Library includes the class [CommandLine](https://developer.apple.com/documentation/swift/commandline) which includes the variable arguments, an array of strings of all arguments passed to the script.

Using this final method to script looks like this:

	#!/usr/bin/swift

	import Foundation

	func runCommand(command: String, wait: Bool = true) {
		let cli = Process()
		cli.launchPath = "/bin/bash"
		cli.arguments = ["-c", command]
		cli.launch()
		if wait {
			cli.waitUntilExit()
			if cli.terminationStatus != 0 {
				print("Error: \(cli.terminationReason)")
			}
		}
	}

	for argument in CommandLine.arguments[1...] {
		let newFileName: String
		let oldFileName: String = argument.lowercased()

		newFileName = String(oldFileName.dropLast(4)) + (oldFileName.contains(".jpg") ? "-new.jpg" : ".jpg")
		print("Converting \(argument)")
		runCommand(command: "convert \"\(argument)\" pnm:- | mozcjpeg -quality 85 > \"\(newFileName)\"")
	}

## Embedding AppleScript 

Another option I explored was to use Swift to pass commands to [AppleScript](https://en.wikipedia.org/wiki/AppleScript) in place of Bash. The [NSAppleAppleScript](https://developer.apple.com/documentation/foundation/nsapplescript) class provides the functionality for this and it is simpler to work with than passing Bash commands. To use it, just all of an instance of the class like this:

	var errors: NSDictionary?
	let script = NSAppleScript(source: String)
	script?.executeAndReturnError(&errors)

In this call, source is a string with the AppleScript code. This can be calculated and played with in a similar manner to crafting the above Bash commands. When the script is ready to be run, the executeAndReturnError function will do just that and return any errors to the errors dictionary. These can be referenced later if desired.

## Conclusion

Using the above methods, scripting with Swift is quite powerful. I have already begun to replace other scripts of mine using this, and as I get into more advanced ones, Swift provides the same sort of APIs as Python for interacting with the computer.

With regards to performance, I have found that Swift is faster in some ways than Python, but also with some performance costs. The Swift REPL is slower to start up than the Python interpretor is, so on my 2014 Mac Mini, Swift scripts take about half a second before they start computing, and a little longer if I am importing Foundation or other Apple frameworks. Subsequent runs of a script are much faster due to I assume how macOS keeps recently used applications loaded in memory. For computationally heavy tasks, I have found that Swift scripts can run faster than Python, although these types of scripts are ones I do not commonly write. Another speed comparison is with [Julia](https://en.wikipedia.org/wiki/Julia_(programming_language)), which has similar start up times and computation speeds.

For myself, Swift is ready to fill the scripting role in my life. Python is a more concise language, but Swift's syntax makes for a clean scripting environment. Swift support in editors such as [Atom](https://atom.io), [Sublime Text](https://www.sublimetext.com), and [Visual Studio Code](https://code.visualstudio.com) are getting better, allowing for the creation of Swift scripts without the need for a heavy IDE like [AppCode](http://www.jetbrains.com/objc) or [Xcode](https://developer.apple.com/xcode). And as I have already done with one script of mine, when the script is getting to a point where compiling it would be advantageous, it is easy to compile the script with the *swiftc* command and then have an executable that will run faster than the REPL.
