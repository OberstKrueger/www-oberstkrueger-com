---
created: 2017-06-20T16:15:00Z
title: About
description: About me and my little corner of the internet.
updated: 2023-04-29T08:40:00Z
---

Welcome to my little corner of the internet.

This site has existed in many forms over the years, starting out as a simple blog built with [Ghost](https://ghost.org), turning into a larger website that I thought of as an online book, and now back in a slightly more minimal form.

This current iteration is influenced by the idea of a *digital garden*, which is the concept of having a website with articles but not structured like a blog. The articles are evergreen, and can go back and be updated as time goes on. It does not preclude a more blog-like section for updates or other uses, but that is not the focus of the website. The previous version of this site, The Krueger Report, was similar in concept, but what I wrote was still more blog-like. The pages did not fit well with being more long-standing ideas to be updated as time went on and more information was learned. This is the main idea idea I am aiming to correct.

Additionally, this site now exists as the main hub for my online presence. Everything else is both linked to by this site as well as linking back to it. All of my main online accounts will have this two-way street, making verification of who I am easier.

## Tools Used To Create This

There are two major tools used to make everything you read here: [Markdown](http://daringfireball.net/projects/markdown/) for the writing, and [Caddy](https://caddyserver.com) for compiling it.

Markdown is a form of markup designed by [John Gruber](http://daringfireball.net) and [Aaron Swartz](http://www.aaronsw.com). The advantages of Markdown for writing is that it is a plain text format that makes converting to other formats simple. There are many tools for converting Markdown to HTML and PDF, where the final output can be easily stylized. And since it is stored in plaintext, it can be created and edited in any number of text editors. Currently, I switch between [iA Writer](https://ia.net/writer) and [Sublime Text](https://www.sublimetext.com) for all Markdown writing.

All of these Markdown files are then served through Caddy, a web server written in [Go](https://golang.org). Caddy has built-in support for rendering Markdown files to HTML using a basic template system. While it is not as powerful as [Hugo](https://www.gohugo.io) or [Zola](https://www.getzola.org), it fulfills my needs, and I would be using Caddy even without the Markdown support as it supports negotiating SSL certificates through [Let's Encrypt](https://letsencrypt.org) automatically.

Every file used for this site is [hosted on GitHub](https://github.com/OberstKrueger/www-krueger-report). Updates are pushed directly to that repository, which Caddy pulls from to update the website. The only aspect of the site that does not change is the HTML portion of theme. Unfortunately, Caddy must be restarted for this to update, although it is rarely an issue as my theme is rarely updated.

One of my goals is for this site to render as quickly as possible. To test this, I use [Yellow Lab Tools](http://yellowlab.tools/) to see detailed metrics about my site. When building and updating the theme, I test against the site index to see the minimum downloaded code for each page. My goal is to keep the base CSS and HTML below 8k, allowing my longest articles to have their text downloaded on [even the slowest of connections](https://danluu.com/web-bloat/). Other metrics presented by Yellow Lab Tools point out any problems with the theme, whether it is overly complex CSS rules or server configuration issues. Images are served as lossly compressed [WebP](https://en.wikipedia.org/wiki/WebP). The files are slightly smaller than the JPEGs that were used previously, but the quality of the images is much higher. All images are lazy loaded for browsers that support the functionality.

