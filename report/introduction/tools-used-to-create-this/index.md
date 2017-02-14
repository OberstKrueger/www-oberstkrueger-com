---
category: introduction
created: 2016.12.10:1010
title: The Krueger Report - Tools Used To Make This
type: page
updated: 2017.02.13:1800
---

# Tools Used To Make This

There are two major tools used to make everything you read here: [Markdown](http://daringfireball.net/projects/markdown/) for the writing, and [Caddy](https://caddyserver.com) for compiling it.

Markdown is a form of markup designed by [John Gruber](http://daringfireball.net) and [Aaron Swartz](http://www.aaronsw.com). The advantages of Markdown for writing is that it is a plain text format that makes converting to other formats very simple. There are many tools for converting Markdown to HTML and PDF, where the final output can be more easily stylized. And since it is stored in plaintext, it can be created and edited in any number of text editors. Currently, I switch between [iA Writer](https://ia.net/writer) and [Sublime Text](https://www.sublimetext.com) for all Markdown writing.

All of these Markdown files are then served through Caddy, a new web server written in [Go](https://golang.org). Caddy has built-in support for rendering Markdown files to HTML using a basic template system. While it is not as powerful as [Ghost](https://ghost.org) or [Hugo](https://www.gohugo.io), it fulfills my needs, and I would be using Caddy even without the Markdown support as it supports negotiating SSL certificates through Let's Encrypt automatically.
