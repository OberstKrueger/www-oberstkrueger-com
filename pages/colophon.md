---
created: 2023-04-29T08:45:00Z
title: Colophon
description: Information about the technology stack behind this website.
updated: 2023-04-29T08:45:00Z
---

> A page on a website identifying the details of its creation, such as the author's name and the technologies used.
>
> -Wiktionary definition of *colophon*

There are two major tools used to make everything you read here: [Markdown](http://daringfireball.net/projects/markdown/) for the writing, and [Caddy](https://caddyserver.com) for compiling it.

Markdown is a form of markup designed by [John Gruber](http://daringfireball.net) and [Aaron Swartz](http://www.aaronsw.com). The advantages of Markdown for writing is that it is a plain text format that makes converting to other formats simple. There are many tools for converting Markdown to HTML and PDF, where the final output can be easily stylized. And since it is stored in plaintext, it can be created and edited in any number of text editors. Currently, I switch between [iA Writer](https://ia.net/writer) and [Sublime Text](https://www.sublimetext.com) for all Markdown writing.

All of these Markdown files are then served through Caddy, a web server written in [Go](https://golang.org). Caddy has built-in support for rendering Markdown files to HTML using a basic template system. While it is not as powerful as [Hugo](https://www.gohugo.io) or [Zola](https://www.getzola.org), it fulfills my needs, and I would be using Caddy even without the Markdown support as it supports negotiating SSL certificates through [Let's Encrypt](https://letsencrypt.org) automatically.

Every file used for this site is [hosted on GitHub](https://github.com/OberstKrueger/www-oberstkrueger-com). Updates are pushed directly to that repository, which the server pulls from to update the website. Images are compressed using the latest compression formats that allow viewing of this website with browsers released in the last 2-4 years. Due to these images being large and regularly updated, they are not a part of the git repo but synced separately.
