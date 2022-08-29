---
created: 2017-06-20T16:15:00Z
title: Hello, World!
type: page
updated: 2022-08-29T09:10:00Z
---

Hello, and welcome to The Krueger Report!

This site has existed for a couple of years now, in various forms. It started out as a simple blog, more as a way to test out [Ghost](https://ghost.org) than a serious attempt at writing. As time went on, I remembered how much I enjoyed writing back in college and wanted to keep it up. As the blog format was not quite right for me, I altered this site to my own custom solution and reshaped it into that of a book. I like the idea of a book more, as it's something I could theoretically compile to an [EPUB](https://en.wikipedia.org/wiki/EPUB) or other e-book format, or even print, and I could have a snapshot of my life at that point.

A recent realization I had was that what I essentially wanted was two types of books: one private and one public. The Krueger Report fills the need of the public notebook, including everything I have written to (sometimes near) completion. The private book consists of notes to myself. I have recently set about the goal that most things put into the private notes will be fodder for content for the public book, whether it be writing about a game that I love or my thought process for choosing a [backup solution for all of my technology](/backups).

In essence, this means that the site is a a running knowledge-base for my life. Anything that I feel has been useful for myself might also be of use to someone else. Therefore it makes sense for that information to be available in a public form.

A separate updates section is present that sort of is blog-like, although I don't write the final thoughts there. This exists as a sort of changelog, highlighting new pages and major updates to old pages.

I hope you enjoy what you find here, or at least find new ideas for yourself here.

## Tools Used To Create This

There are two major tools used to make everything you read here: [Markdown](http://daringfireball.net/projects/markdown/) for the writing, and [Caddy](https://caddyserver.com) for compiling it.

Markdown is a form of markup designed by [John Gruber](http://daringfireball.net) and [Aaron Swartz](http://www.aaronsw.com). The advantages of Markdown for writing is that it is a plain text format that makes converting to other formats simple. There are many tools for converting Markdown to HTML and PDF, where the final output can be easily stylized. And since it is stored in plaintext, it can be created and edited in any number of text editors. Currently, I switch between [iA Writer](https://ia.net/writer) and [Sublime Text](https://www.sublimetext.com) for all Markdown writing.

All of these Markdown files are then served through Caddy, a web server written in [Go](https://golang.org). Caddy has built-in support for rendering Markdown files to HTML using a basic template system. While it is not as powerful as [Hugo](https://www.gohugo.io) or [Zola](https://www.getzola.org), it fulfills my needs, and I would be using Caddy even without the Markdown support as it supports negotiating SSL certificates through [Let's Encrypt](https://letsencrypt.org) automatically.

Every file used for this site is [hosted on GitHub](https://github.com/OberstKrueger/www-krueger-report). Updates are pushed directly to that repository, which Caddy pulls from to update the website. The only aspect of the site that does not change is the HTML portion of theme. Unfortunately, Caddy must be restarted for this to update, although it is rarely an issue as my theme is rarely updated.

One of my goals is for this site to render as quickly as possible. To test this, I use [Yellow Lab Tools](http://yellowlab.tools/) to see detailed metrics about my site. When building and updating the theme, I test against the site index to see the minimum downloaded code for each page. My goal is to keep the base CSS and HTML below 8k, allowing my longest articles to have their text downloaded on [even the slowest of connections](https://danluu.com/web-bloat/). Other metrics presented by Yellow Lab Tools point out any problems with the theme, whether it is overly complex CSS rules or server configuration issues. Images are served as lossly compressed [WebP](https://en.wikipedia.org/wiki/WebP). The files are slightly smaller than the JPEGs that were used previously, but the quality of the images is much higher. All images are lazy loaded for browsers that support the functionality.

