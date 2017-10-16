---
category: notes-on-books
created: 2017.10.16:1100
title: Resilient Web Design
type: page
updated: 2017.10.16:1335
---

**Title**: Resilient Web Design<br>
**Author**: Jeremy Keith<br>
**Author's Background**: Web developer; Homebrew Website Club organizer in Brighton, UK; works at Clearleft, a design agency in the UK

### Notes

- All technological progress depends on some form of past progress. i.e. Gutenberg's press was built on top of knowledge gained by the creation of the wine screw press, and UI icons that use past physical items, i.e. "save" icon being a floppy disk.
- The Internet's decentralized design was not to prevent being knocked out by nuclear war, but to prevent total censorship.
- HTML and CSS are designed purposefully to not error out when encountering new elements and values. That way, new features can be added and older browsers that don't recognize them can still display something, even if it wasn't the intended effect. This makes web pages more resilient.
- Internet Explorer 5 for Mac was the first browser to launch with extensive CSS support, despite Internet Explorer for Windows not fully supporting it.
- HTML and CSS depending on each other and each providing their own focused attributes follows the UNIX philosophy of each tool doing one thing. This split isn't 100%, as HTML often has to include certain identifiers for CSS, in the form of class and id tags.
- *Material honesty* is using a material for its intended purpose, and not for anything else. A web design example of this is using tables for overall page layout, and not simply as a table of data.
- HTML is materially honest if it is solely content, and CSS is materially honest if it is solely design.
- The first web page layouts tried to mimic that of print layout. Designs were often fixed, and built upon the same principles that print designers have used for hundreds of years. The problem though is that a web browser window from the beginning does not have a fixed size, a problem that is made worse today due to the number of mobile devices of various sizes.
- Before mobile layouts, web designers fixed on websites generally being 960 pixels wide.
- Much like how early movies mimicked the theater and early television mimicked the radio, early web design mimicked print design.
- The first tools used for web design were ones like Photoshop, tools focused on designs with fixed constraints.
- The iPhone's mobile browser changed everything. It forced designers and developers to consider whether users were using a high resolution screen to view their site or a tiny 320 pixel-wide phone to do so, and whether they are using a fast home Internet connection or a slow mobile network.
- The first solution to the mobile device problems was to simply punt mobile users to a separate "mobile-optimized" site. This method breaks down with the proliferation of devices beyond just the iPhone: tablets, TV browsers, and future devices we've yet to create.
- Ethan Marcotte's call to use *responsive web design* was well received in 2010. It built on top of web technologies already created: fluid elements, images, and media queries.
- *Mobile first* design methodology arose, since parring down a desktop site does not always work. Designers began to build up from mobile, and not down from desktop.
- JavaScript was created by Netscape employee Brendan Each in 1996. It was created in 10 days.
- JavaScript does not treat errors the same way as CSS and HTML. If a JavaScript file has an error, even a small typo, it will stop running once it hits that error.
- XHTML brought imperative-style error responses to HTML. Now, whole web pages would stop rendering if there was a single error of any kind in the HTML. It did not go over well, and modern HTML acts the same as the original versions of HTML.
- Every design does not need to be rendered pixel-perfect on every browser. Good design will take advantage of as many new features as it wants, but will still gracefully fall back to eventually being nothing but basic HTML, and still function properly. Trying to force pixel-perfect designs on web pages is the same as trying to force print designs on the web.
- Progressive enhancement does not mean every browser must support every feature. Core functionality must be split from enhanced functionality, the latter of which does not need to be guaranteed to every user.

### Quotes

> Design adds clarity. Using colour, typography, hierarchy, contrast, and all the other tools at their disposal, designers can take an unordered jumble of information and turn it into something that’s easy to use and pleasurable to behold. Like life itself, design can win a small victory against the entropy of the universe, creating pockets of order from the raw materials of chaos.

<div></div>

> JavaScript gave web designers the power to create websites that were slicker, smoother, and more reactive. The same technology also gave web designers the power to create websites that were sluggish, unwieldy, and more difficult to use.

<div></div>

> This doesn’t mean that web designers shouldn’t use JavaScript. But it does mean that web designers shouldn’t rely on JavaScript when a simpler solution exists.

<div></div>

> Here’s a three-step approach I take to web design:
> 
> 1. Identify core functionality.
> 2. Make that functionality available using the simplest possible technology.
> 3. Enhance!
> 
> Identifying core functionality might sound like it’s pretty straightforward, and after a bit of practice, it is. But it can be tricky at first to separate what’s truly necessary from what’s nice to have.

### Further Reading

- [A Dao of web design](https://alistapart.com/article/dao)
- [Openness and the metaverse singularity](http://www.kurzweilai.net/openness-and-the-metaverse-singularity)
- [Responsive web design](https://alistapart.com/article/responsive-web-design)
- [Do websites need to look exactly the same in every browser?](http://dowebsitesneedtolookexactlythesameineverybrowser.com)
- [Support vs optimization](http://bradfrost.com/blog/mobile/support-vs-optimization/)
- [Future Friendly](http://futurefriendlyweb.com)
