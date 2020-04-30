---
category: programming
created: 2018-07-21T00:30Z
title: Exit Status Codes
type: page
updated: 2019-02-25T00:35Z
---

On all [Unix](https://en.wikipedia.org/wiki/Unix) operating systems, every time a process exits, it returns an [exit status](https://en.wikipedia.org/wiki/Exit_status) that tells the operating system whether the process ran successfully or encountered some sort of failure mode. Implementing these exit statuses is important so that the tool can interact with the rest of the system in an expected way.

The [POSIX](https://en.wikipedia.org/wiki/POSIX) standards declares that the exit status for an executable is a 32-bit integer, meaning the value can be between 0 and 2,147,483,647. [The Single Unix Specification](http://www.unix.org/what_is_unix/single_unix_specification.html) declares that an exit status only pulls from the final 8-bits of whatever exit status is presented, effectively making it an 8-bit unsigned integer. Since most tools created are aiming to target systems that follow both the POSIX standard and the Unix standard, restricting the exit status to being 0 through 255 allows for the best compatibility.

## Zero and Non-Zero

Both standards state that an exit status of zero means the executable exited in a successful state, and any other non-zero exit status means that an error occurred. [The C programming language](https://en.wikipedia.org/wiki/C_(programming_language)) has two constants called EXIT\_SUCCESS and EXIT\_FAILURE that [respectively map to the values of 0 and 1](https://www.gnu.org/software/libc/manual/html_node/Exit-Status.html). Most languages build similar values into their own standard libraries, creating the de facto standard of 0 equaling success and 1 equaling an error.

## Beyond Just Zero and One

Knowing whether a tool is successful or not is important, but providing more information to the rest of the system has many advantages. Unfortunately, there are no universal standards for exit codes that go beyond the standard failure code.

The closest there is to an official extended standard comes from the [BSD family of operating systems](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution). The header file [sysexits.h](https://github.com/openbsd/src/blob/master/include/sysexits.h) defines 15 new error statuses in the range of 64 to 78. These include options for returning based on both system errors and user errors. Unlike with C, sysexits.h does not declare 1 as the generic failure exit status, but instead covers most needs under the new statuses. The exit statuses provided by sysexits.h are as follows:

- 64 - Command line usage error
- 65 - Data format error
- 66 - Input is not openable
- 67 - Addressee unknown
- 68 - Unknown host name
- 69 - Service unavailable
- 70 - Internal software error
- 71 - System error
- 72 - Critical OS file missing
- 73 - Can no create output file
- 74 - I/O error
- 75 - Temporary failure
- 76 - Remote error in protocol
- 77 - Permission denied
- 78 - Configuration error

[GNU grep](https://www.gnu.org/software/grep/) includes one additional exit status. Grep will return 2 if there is any sort of I/O error experienced while processing the command.

The [Bash Reference Manual](https://www.gnu.org/software/bash/manual/html_node/index.html) adds three additional exit statuses. 2 is returned if the command called is used incorrectly, such as not providing an input or misusing an argument. 126 is returned if command exists but is not executable(for example, if the command does not have correct permission levels), and 127 is returned if the command is not found. Neither of these last two exit statuses would be valid for an executable to itself return, although they can be useful in processing the exit status of other subprocesses of the executable.

Mendel Cooper, author of the [Advanced Bash-Scripting Guide](https://www.tldp.org/LDP/abs/html/) adds a few additional exit statuses on top of the Bash standards: 128 to indicated an invalid exit code, 130 to indicated that the user interrupted the process with Ctrl-C, and anything above 128 indicates a fatal error signal, such as 137(128 + 9) indicated a kill signal 9 being passed to the process. Any exit code above 255 is considered out of range and invalid. Just like the above Bash statuses, these are useful for processing other processes statuses but not being passed by the command run.

## List of Exit Statuses

Amongst all of these proposed exit codes, there is only one conflict. Both grep and Bash define status 2 for competing purposes. Since there is no standard that says which is correct, the safest best is to not expect 2 to always mean one or the other. If you remove this duplicate, you are left with the following list of exit codes.

- 0 - Successful termination
- 1 - Unspecified error
- 2 - Incorrect command usage or I/O error
- 64 - Command line usage error
- 65 - Data format error
- 66 - Input is not openable
- 67 - Addressee unknown
- 68 - Unknown host name
- 69 - Service unavailable
- 70 - Internal software error
- 71 - System error
- 72 - Critical OS file missing
- 73 - Can no create output file
- 74 - I/O error
- 75 - Temporary failure
- 76 - Remote error in protocol
- 77 - Permission denied
- 78 - Configuration error
- 126 - Command found but not executable
- 127 - Command not found
- 128 - Invalid exit code
- 128 + n - Fatal error signal n, i.e. kill -9 $PPID (128 + 9 = 137)
- 130 - Command terminated by Ctrl-C
- 255+ - Exit code out of range

It is important to reiterate that outside of 0 meaning the command executed successfully and any other value indicating an error, these are not standard statuses to use across all systems. Some are considered safer to use than others, such as the BSD exit statuses being used in other operating systems like macOS, but none of them are hard standards. Following them is helpful, but any code written with exit codes other than 0 and 1 should include documentation about what the exit codes mean.
