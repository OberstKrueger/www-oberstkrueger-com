---
category: technology
created: 2018.04.25:0325
title: CLI Tools
type: page
updated: 2018.05.12:0755
---

For most people, a [command-line interface](https://en.wikipedia.org/wiki/Command-line_interface) is a product of a bygone era of computing. Computer users up through the 1990s had to be comfortable with a command-line in either [DOS](https://en.wikipedia.org/wiki/DOS) or [Unix](https://en.wikipedia.org/wiki/Unix) forms, but since then, [graphical interfaces](https://en.wikipedia.org/wiki/Graphical_user_interface) have been how most people interact with a computer. This is emphasized in many modern devices like smartphones and tablets where a command-line interface would be difficult to use due to the onscreen keyboard.

Despite the power of modern graphical interfaces, command-line tools are still worth exploring. Many programming tools are primarily used through a command-line, and tying multiple tools together using a [shell script](https://en.wikipedia.org/wiki/Shell_script) provides customizability that most graphical tools can not recreate.

I remain a huge fan of command-lines. Most of my desktops on macOS have a terminal present, and I have one desktop dedicated to a full-screen instance of [Alacritty](https://github.com/jwilm/alacritty) that I use for writing and other various uses. Below are some of my favorite tools to use, along with basic some of my most commonly used commands.

## bat

**Site**: [https://github.com/sharkdp/bat](https://github.com/sharkdp/bat)<br>
**Summary**: Clone of cat with syntax highlighting and Git integration

- Display contents of a single file
    - bat file
- Specify language for syntax highlighting
    - bat file -l language

## cloc

**Site**: [https://github.com/AlDanial/cloc](https://github.com/AlDanial/cloc)<br>
**Summary**: Statistics utility to count lines of code

- Count all the lines of code in a directory:
	- cloc /path/to/directory
- Count all the lines of code in a directory, displaying a progress bar during the counting process:
	- cloc --progress=1 /path/to/directory
- Compare 2 directory structures and count the differences between them:
	- cloc --diff /directory/one /directory/two

## dtrx

**Site**: [https://brettcsmith.org/2007/dtrx/](https://brettcsmith.org/2007/dtrx/)<br>
**Summary**: Intelligent archive extraction

- Extract all files:
	- dtrx file
- Extra all files to current directory:
	- dtrx -f

## fd

**Site**: [https://github.com/sharkdp/fd](https://github.com/sharkdp/fd)<br>
**Summary**: A simple, fast and user-friendly alternative to 'find'

- Find files under current directory that match a pattern:
	- fd pattern
- Find files with a specific extension:
	- fd -e .ext pattern
- Find files and execute on the results:
	- fd pattern -x command

## ffmpeg

**Site**: [https://ffmpeg.org/](https://ffmpeg.org/)<br>
**Summary**: Play, record, convert, and stream audio and video

- Extract the sound from a video and save it as MP3:
	- ffmpeg -i video.mp4 -vn sound.mp3
- Convert frames from a video or GIF into individual numbered images:
	- ffmpeg -i video.mpg|video.gif frame_%d.png
- Combine numbered images (frame_1.jpg, frame_2.jpg, etc) into a video or GIF:
	- ffmpeg -i frame_%d.jpg -f image2 video.mpg|video.gif
- Quickly extract a single frame from a video at time mm:ss and save it as a 128x128 resolution image:
	- ffmpeg -ss mm:ss -i video.mp4 -frames 1 -s 128x128 -f image2 image.png
- Convert AVI video to MP4. AAC Audio @ 128kbit, h264 Video @ CRF 23:
	- ffmpeg -i input_video.avi -codec:audio aac -b:audio 128k -codec:video libx264 -crf 23 output_video.mp4
- Remux MKV video to MP4 without re-encoding audio or video streams:
	- ffmpeg -i input_video.mkv -codec copy output_video.mp4
- Convert MP4 video to VP9 codec. For the best quality, use a CRF value (recommended range 15-35) and -b:video MUST be 0:
	- ffmpeg -i input_video.mp4 -codec:video libvpx-vp9 -crf 30 -b:video 0 -codec:audio libopus -vbr on -threads number_of_threads output_video.webm

## git-sizer

**Site**: [https://github.com/github/git-sizer](https://github.com/github/git-sizer)<br>
**Summary**: Compute various size metrics for a Git repository, flagging those that might cause problems

- Report basic statistics and problems with Git repository:
	- git-sizer
- Report all statistics:
	- git-sizer -v

## lynx

**Site**: [http://lynx.invisible-island.net](http://lynx.invisible-island.net)<br>
**Summary**: Text-based web browser that supports http, gopher, ftp, and telnet

## mas

**Site**: [https://github.com/mas-cli/mas](https://github.com/mas-cli/mas)<br>
**Summary**: Mac App Store command-line interface

- List pending updates from the Mac App Store:
	- mas outdated
- Upgrade outdated apps:
	- mas upgrade

## neofetch

**Site**: [https://github.com/dylanaraps/neofetch](https://github.com/dylanaraps/neofetch)<br>
**Summary**: Fast, highly customisable system info script

## neovim

**Site**: [https://neovim.io](https://neovim.io)<br>
**Summary**: Ambitious Vim-fork focused on extensibility and agility

## pandoc

**Site**: [https://pandoc.org](https://pandoc.org)<br>
**Summary**: Swiss-army knife of markup format conversion

- Convert file to pdf (the output format is automatically determined from the output file's extension):
	- pandoc input.md -o output.pdf
- Convert a file to a specific output format (useful for when the extension alone is ambiguous):
	- pandoc input.docx --to markdown_github -o output.md
- List all supported input formats:
	- pandoc --list-input-formats
- List all supported output formats:
	- pandoc --list-output-formats

## python

**Site**: [https://www.python.org](https://www.python.org)<br>
**Summary**: Interpreted, interactive, object-oriented programming language

- Call a Python interactive shell (REPL):
	- python
- Execute script in a given Python file:
	- python script.py
- Execute Python language single command:
	- python -c command
- Run library module as a script (terminates option list):
	- python -m module arguments

## ranger

**Site**: [https://ranger.github.io](https://ranger.github.io)<br>
**Summary**: A vim-inspired filemanager for the console

## ripgrep

**Site**: [https://github.com/BurntSushi/ripgrep](https://github.com/BurntSushi/ripgrep)<br>
**Summary**: Search tool like grep and The Silver Searcher

- Recursively search the current directory for a regex pattern:
	- rg pattern
- Search for pattern including all .gitignored and hidden files:
	- rg -uu pattern
- Search for a pattern only in a certain filetype (e.g., html, css, etc.):
	- rg -t filetype pattern
- Search for a pattern only in a subset of directories:
	- rg pattern set_of_subdirs
- Search for a pattern in files matching a glob (e.g., `README.*`):
	- rg pattern -g glob

## sassc

**Site**: [https://github.com/sass/sassc](https://github.com/sass/sassc)<br>
**Summary**: Wrapper around libsass that helps to create command-line apps

- Compile Sass file to CSS:
	- sassc input output
- Compile Sass to compact CSS:
	- sassc -t compact input output

## swiftlint

**Site**: [https://github.com/realm/SwiftLint](https://github.com/realm/SwiftLint)<br>
**Summary**: Tool to enforce Swift style and conventions

- Lint Swift files in current directory:
	- swiftlint
- Lint Swift files and automatically correct errors and warnings:
	- swiftlint autocorrect

## tldr

**Site**: [https://tldr.sh/](https://tldr.sh/)<br>
**Summary**: Simplified and community-driven man pages

- Get typical usages of a command (hint: this is how you got here!):
	- tldr command
- Update the local cache of tldr pages:
	- tldr --update

## tmux

**Site**: [https://tmux.github.io/](https://tmux.github.io/)<br>
**Summary**: Terminal multiplexer

- Start a new tmux session:
	- tmux
- Start a new named tmux session:
	- tmux new -s name
- List sessions:
	- tmux ls
- Attach to a named session:
	- tmux a -t name
- Detach from session:
	- Ctrl + B, D
- Kill session:
	- tmux kill-session -t name

## tree

**Site**: [http://mama.indstate.edu/users/ice/tree/](http://mama.indstate.edu/users/ice/tree/)<br>
**Summary**: Display directories as trees

- Show files and directories up to a certain number of levels:
	- tree -L number
- Show directories only:
	- tree -d
- Show hidden files:
	- tree -a

## webkit2png

**Site**: [http://www.paulhammond.org/webkit2png/](http://www.paulhammond.org/webkit2png/)<br>
**Summary**: Create screenshots of webpages from the terminal

- Render a screenshot of a webpage:
	- webkit2png https://website
- Render a screenshot with the desired dimensions:
	- webkit2png -W width -H height https://website
- Render a screenshot at a higher DPI:
	- webkit2-png -z 2 https://website

## wget

**Site**: [https://www.gnu.org/software/wget/](https://www.gnu.org/software/wget/)<br>
**Summary**: Internet file retriever

- Download the contents of an URL to a file (named "foo" in this case):
	- wget https://example.com/foo
- Download the contents of an URL to a file (named "bar" in this case):
	- wget -O bar https://example.com/foo
- Download a single web page and all its resources (scripts, stylesheets, images, etc.):
	- wget --page-requisites --convert-links https://example.com/somepage.html
- Download a full website, with 3-second intervals between requests:
	- wget --mirror --page-requisites --convert-links --wait=3 https://example.com
- Download all listed files within a directory and its sub-directories (does not download embedded page elements):
	- wget --mirror --no-parent https://example.com/somepath/
- Download the contents of an URL via authenticated FTP:
	- wget --ftp-user=username --ftp-password=password ftp://example.com
- Limit download speed to 200 kB/s:
	- wget --limit-rate=200k https://example.com
- Continue an incomplete download:
	- wget -c https://example.com
- Retry a given number of times if the download doesn't succeed at first:
	- wget -t number_of_retries https://example.com

## youtube-dl

**Site**: [https://rg3.github.io/youtube-dl/](https://rg3.github.io/youtube-dl/)<br>
**Summary**: Download Youtube videos from the command-line

- Download a video or playlist:
	- youtube-dl https://www.youtube.com/watch?v=oHg5SJYRHA0
- Download the audio from a video and convert it to an MP3:
	- youtube-dl -x --audio-format mp3 url
