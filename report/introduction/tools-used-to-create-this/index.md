---
category: introduction
created: 2016.12.10:1010
title: The Krueger Report - Tools Used To Make This
type: page
updated: 2017.04.01:1800
---

# Tools Used To Make This

There are two major tools used to make everything you read here: [Markdown](http://daringfireball.net/projects/markdown/) for the writing, and [Caddy](https://caddyserver.com) for compiling it.

Markdown is a form of markup designed by [John Gruber](http://daringfireball.net) and [Aaron Swartz](http://www.aaronsw.com). The advantages of Markdown for writing is that it is a plain text format that makes converting to other formats very simple. There are many tools for converting Markdown to HTML and PDF, where the final output can be more easily stylized. And since it is stored in plaintext, it can be created and edited in any number of text editors. Currently, I switch between [iA Writer](https://ia.net/writer) and [Sublime Text](https://www.sublimetext.com) for all Markdown writing.

All of these Markdown files are then served through Caddy, a new web server written in [Go](https://golang.org). Caddy has built-in support for rendering Markdown files to HTML using a basic template system. While it is not as powerful as [Ghost](https://ghost.org) or [Hugo](https://www.gohugo.io), it fulfills my needs, and I would be using Caddy even without the Markdown support as it supports negotiating SSL certificates through [Let's Encrypt](https://letsencrypt.org) automatically.

Every file used for this site is [hosted on GitHub](https://github.com/OberstKrueger/the-krueger-report). Updates are pushed directly to that repository, which Caddy pulls from to update the website. The only aspect of the site that does not change is the HTML portion of theme. Unfortunately, Caddy must be restarted for this to update, although it is rarely an issue as my theme does not see many changes.

One of my goals is for this site to render as quickly as possible. To test this, I use [Yellow Lab Tools](http://yellowlab.tools/) to see detailed metrics about my site. When building and updating the theme, I test against the site index to see the minimum downloaded code for each page. My goal is to keep the base CSS and HTML below 8k, allowing my longest articles to have their text downloaded on [even the slowest of connections](https://danluu.com/web-bloat/). Other metrics presented by Yellow Lab Tools point out any problems with the theme, whether it is overly complex CSS rules or server configuration issues.
