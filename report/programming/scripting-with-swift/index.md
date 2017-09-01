---
category: programming
created: 2017.08.26:1615
title: Scripting With Swift
type: page
updated: 2017.09.01:0545
---

One of the strengths of any [Unix](https://en.wikipedia.org/wiki/Unix)-based operating system is the ability to automate it using custom scripts. A typical script is created using [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) or [Python](https://en.wikipedia.org/wiki/Python_(programming_language)) and run through the terminal or automated using something like systemd or launchd.

Since it's release, one of the interesting prospects of [Swift](https://en.wikipedia.org/wiki/Swift_(programming_language)) has been its use as a scripting language. While Swift is a lower-level language than Python, it's tight integration with [macOS APIs](https://developer.apple.com/documentation/) would allow it to be used to fill this purpose. Simplifying matters is the fact that Swift includes a [REPL](https://en.wikipedia.org/wiki/Read–eval–print_loop), allowing Swift files to be passed in and ran without the need to compile them before running. This allows for faster development and testing of any Swift scripts, and makes it possible to run them without worrying whether they are compiled for the architecture they will be running on.

My current setup is to use Bash for any script that is a list of commands without any scripting logic need, and to use Python for any script that requires any sort of logic or text manipulation. As an experiment, I looked at converting basic Python scripts to Swift.

## Test Script - Converting PNGs To JPGs Using Mozjpeg

The first script that I wanted to convert is a simple Python script that converts [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) images to [JPEG](https://en.wikipedia.org/wiki/JPEG) images optimized for web usage using the [Mozjpeg](https://github.com/mozilla/mozjpeg) encoder. This is a common script I use for web development, as the Mozjpeg encode is one of the most efficient about there.

Mozjpeg does not contain a general purpose image decoder. If you are passing anything other than a JPEG to it, the image will need to first be prepared by another tool. [ImageMagick](https://en.m.wikipedia.org/wiki/ImageMagick) is capable of decoding most image formats available and can convert an image into an intermediary format that Mozjpeg will understand. This two-step process of converting to an intermediary format and then encoding to JPEG is a perfect candidate for scripting, as the full Bash command for the conversion is long:

	convert image.png pnm:- | mozcjpeg -quality 85 > image.png

When the script is run, it accepts PNG images as parameters. The script works in the following manner:

1. Calculate the new file name, swapping the extension "png" with "jpg".
2. Create the Bash command as a string, inserting the original file name and new file name in the appropriate spots.
3. Pass this command to Bash, which runs it.
4. Repeat for as many JPEGs are passed to it.

My original script in Python looks like this.

	#!/usr/bin/env python3
	
	from sys import argv
	from os import system
	
	for arg in argv[1:]:
		new_file_name = "{}jpg".format(arg[:-3])
		command = "convert \"{}\" pnm:- | mozcjpeg -quality 85 > \"{}\"".format(arg, new_file_name)
		system(command)

This script makes for a good test case for Swift for a few reasons. First, it is a simple script with minimal logic used. Second, it does not interact with files directly, instead reading input from passed arguments and then passing a command back to the terminal to be run by it. Like with Python, interacting with files directly is possible with Swift, but given that most of my current scripts interact using Bash commands, I wanted to stick with that first.

Python's point of interaction with the terminal is through [os.system](https://docs.python.org/3.5/library/os.html#os.system). Swift has a few different ways it can interface with the terminal, with the main one being the [Process](https://developer.apple.com/documentation/foundation/process) class within Foundation. This class has a few different commands, but the simplest way for this to work is to set the launchPath and argument variables, and then use the launch() and waitUntilExit() functions. The launchPath variable accepts a string pointing to the command that the script wants to run. The arguments variable accepts an array of strings with the arguments that are passed to the command. The launch() runs the command defined within launchPath with arguments passed to it. And finally, waitUntilExit() pauses the script until the command run is complete. Without this final function, the command will run in the background and the script will lose control of being able to interact with it further.

This class is not one that seems to be used that much, as there are not that many questions about it. Most of the questions and solutions posted on Stack Overflow about it use it in the following manner.

	let task = Process()
	task.launchPath = "/usr/bin/"
	task.arguments = ["ls", "-l"]
	task.launch()
	task.waitUntilExit()

This setup works fine if you are passing simple commands to the terminal with one or two arguments, but it does not work for the above command. Anything with complex piping and symbols breaks this function. No combination of strings for the argument variable would make this work.

Another failed method that I tried was to point launchPath to the convert binary and pass the rest of the command as arguments for that. When this script ran, it would run the convert binary, but none of the arguments were passed. Closer, but still not what I needed.

After a few hours of research, the solution to my problem was to point launchPath to Bash itself, and then pass the command using the argument "-c". According to the [Bash manual](https://www.gnu.org/software/bash/manual/bash.html), what this does is send the whole string to Bash to be run as it is entered. It ends up working the same as typing that command into the terminal. After using Swift to craft the full command to be passed, this method produced the desired output.

The last piece needed to complete the script is to accept arguments from the command-line when the script is run. This was easier to figure out than passing commands, as the Swift Standard Library includes the class [CommandLine](https://developer.apple.com/documentation/swift/commandline) which includes the variable arguments, an array of strings of all arguments passed to the script.

Using this final method to script looks like this:

	#!/usr/bin/swift
	
	import Foundation
	
	func runCommand(_ command: String) {
		let cli = Process()
		cli.launchPath = "/bin/Bash"
		cli.arguments = ["-c", command]
		cli.launch()
		cli.waitUntilExit()
	}
	
	for i in 1..<CommandLine.arguments.count {
		let oldFileName: String = CommandLine.arguments[i]
		let newFileName: String = "\(String(CommandLine.arguments[i].characters.dropLast(3)))jpg"
		print("Converting \(oldFileName)")
		runCommand("convert \"\(oldFileName)\" pnm:- | mozcjpeg -quality 85 > \"\(newFileName)\"")
	}

This script is structured differently than the Python script. The runCommand function does the work of passing the command to the terminal. This function will be reusable, and will form the basis of future scripts in Swift. It functions as described above, accepting a single string and passing that on to Bash.

## Future Alterations

One possibility that I have yet to further explore is the potential of not using waitUntilExit() to speed up short but numerous commands. When I tested this out by removing that line and then running this script against a large number of PNGs, the script would pass the commands to Bash and exit all within a second. If I immediately looked at the size of all of the JPEGs in the directory, they would be zero as the conversion had yet to take place. If I waited a few seconds, they would then show up as the correct size. The conversion was taking place in the background, which was confirmed by looking at the running processes in Activity Monitor.

This opens up the possibility of a crude form of multithreading without the need to manage each individual task. Since the commands are all ran in the background, it's hard to accurately time this through the computer, but just running the commands both with and without waitUntilExit() present, the version without it appeared to run faster based on timing it with my watch.

In the future, the runCommand function could be modified to accept an option argument about whether waiting until completion is necessary. If yes, it will simply pause until the command is complete. If not, it could use Grand Central Dispatch or another proper use of subprocessing to create a new thread and run the command in the background, which would allow the script to retain some control over it.

## launchPath Deprecated?

According to the Swift documentation, the [launchPath variable of Process() is deprecated](https://developer.apple.com/documentation/foundation/process). It still functions in Swift 4, but this does not guarantees its continued functioning in future versions of Swift.

Unfortunately, I was unable to find any reference as to a way to replace this functionality in a new manner. There has been no reference to its deprecation within the Foundation repository on GitHub. For now, this is the best method for this scripting functionality, but it will need to be changed in the future.

## AppleScript As An Alternative?

Another option I explored was to use Swift to pass commands to [AppleScript](https://en.wikipedia.org/wiki/AppleScript) in place of Bash. The [NSAppleAppleScript](https://developer.apple.com/documentation/foundation/nsapplescript) class provides the functionality for this and it is simpler to work with than passing Bash commands. To use it, just all of an instance of the class like this:

	let script = NSAppleScript(source: scriptInput)

In this call, scriptInput is a String with the AppleScript code. This can be calculated and played with in a similar manner to crafting the above Bash commands.

This script work, but what I found was that it was redundant. I was crafting the same AppleScript code and wrapping it up in Swift boilerplate. Additionally, the code executed much slower than if it were run from the AppleScript Editor. In some cases, this speed loss was to the effect of 10 times slower. For single commands, this might be passable but for more advanced scripting that might interact with multiple applications or objects, this is too slow.

AppleScript has its place, but wrapped up in Swift is not one of them, at least for these purposes.

## Conclusion

Using the above Bash method, scripting with Swift is quite powerful. I have already begun to replace other scripts of mine using this, and as I get into more advanced ones, Swift provides the same sort of APIs as Python for interacting with the computer.

For myself, Swift is ready to fill this role. Python is a more concise language, but Swift's syntax makes for a very clean scripting environment. Swift support in editors such as [Atom](https://atom.io), [Sublime Text](https://www.sublimetext.com), and [Visual Studio Code](https://code.visualstudio.com) are getting better, allowing for the creation of Swift scripts without the need for a heavy IDE like [AppCode](http://www.jetbrains.com/objc) or [Xcode](https://developer.apple.com/xcode).

It will be some time before all of my scripts are converted from Python to Swift. But every script I make in the future will be done in Swift, without exception.