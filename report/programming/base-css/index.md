---
category: programming
created: 2017.08.06:1745
title: base-css
type: page
updated: 2017.09.01:0545
---

I have never been keen to using larger full-featured web frameworks like [Bootstrap](https://en.wikipedia.org/wiki/Bootstrap_(front-end_framework)). While Bootstrap provides a lot of advanced features, CSS Has something that I have always enjoyed crafting by hand. At the same time, most of my projects start with me taking some boilerplate from previous projects and then building on top of that. Up until now, I have not have a specific source of this boilerplate that I pulled from. To rectify this, I created base-css.

base-css is going to be the core of the CSS that I use for all projects going forward. It is opinionated in many ways, but also setup in a way where those opinions can be overridden without any significant amount of work. Its focus is on setting a standardized typographic look across all platforms, leaving layout and other such tasks to project-specific CSS that will be filled in later.

### Typography

The goal is to be good looking uniform typography that still fits in with the environment it is being viewed on. Web fonts would help with this, but the goal is to keep this small, so that if the default stack is used, it adds as little overhead as possible. To accomplish this, I chose what I felt were the best fonts available on all of the major platforms. That way, each system has a font that looks good on it without having to worry about falling back to the system default. To that end, the fonts used are Avenir Next for Apple systems, Open Sans for Android systems, and Segoe UI for Windows systems.

By default, base-css has a tighter line-height than most: 1.375. With a mobile-focused world, it felt right to decrease line size as many people will be reading on smaller devices with shorter lines. Large line-heights can waste space in this reading environment, and when the width is small enough, tracking between lines is not a problem at this particular line-height.

HTML and Markdown provide 6 levels of headers, but I personally feel that that is too many. My own work uses 3 levels at most. To help with accidentally using a deeper level of header, I provided styles only for header levels 1, 2, and 3, with 4, 5, and 6 mirroring how 3 looks.

Basic print styles are included in the elements where it makes sense.

### Figures and images

Another manner in which this file is opinionated is that it is meant to be used with Markdown with a minimal use of custom HTML added in. The exception to this comes to how images are handled. Most Markdown renderers will stick images inside of a p element, which is basic and does not allow for much control over the image. To accommodate for this, I added multiple classes for the figure element to allow for full-width, half-width, and quarter-width images to be floated both to the left and right side of the pages.

### Easily customizable

Many of the features of this CSS is that it can be modified by changing a few variables at the top. All of the key features, such as colors and line-height, use Sass variables. I took into account possible changes, so when the line-height would affect the margin of an option, I used a Sass calculation so that all margins will be adjusted for any changes to the line-height.

To test out how well it works, I recently updated the design of [The Krueger Report](/). base-css provided the foundation for the new update. With the new update, I was able to simply constrain the text in a few ways and ended up with the final product. ⅔ of the code in the new version of this site's CSS is still base-css.

### The code

The full code can be viewed [on GitHub](https://github.com/OberstKrueger/base-css). If you wish to use it, just clone that repo and work away.

Additionally, the entire .scss file can be found below. It was compiled with version 3.4 of Sass, but should work on older versions. The compiled .css file can be found on the above GitHub repository.

	/*
			VARIABLES
	*/
	$colorBackground: rgba(255, 255, 255, 1);
	$colorContainer: rgba(240, 240, 240, 1);
	$colorPrimary: rgba(24, 98, 171, 1);
	$colorSecondary: rgba(43, 138, 62, 1);
	$colorText: rgba(33, 37, 41, 1);
	
	$fontSize: 100%;
	$fontSizePrint: 10pt;
	$fontStack: "Avenir Next", "Avenir", "Open Sans", "Segoe UI", sans-serif;
	$fontStackMono: monospace;
	$fontWeightThick: 700;
	$fontWeightThin: 400;
	
	$lineHeight: 1.375;
	
	/*
			TYPOGRAPHY
	*/
	html {
		font-family: $fontStack;
		font-feature-settings: "dlig" 1, "kern" 1;
		font-size: $fontSize;
		line-height: $lineHeight;
		@media print {
			font-size: $fontSizePrint;
		}
	}
	
	b,
	strong {
		font-weight: $fontWeightThick;
	}
	
	code {
		display: block;
		font-family: $fontStackMono;
		font-size: 0.75rem;
		line-height: $lineHeight / 0.75;
		white-space: pre-wrap;
		word-wrap: break-word;
	}
	
	em {
		font-style: italic;
	}
	
	h1 {
		font-size: 2rem;
		font-weight: $fontWeightThick;
		margin: ($lineHeight * 2rem) auto ($lineHeight * 2rem);
		text-align: center;
		a:link,
		a:visited,
		a:hover,
		a:active {
			color: $colorText;
			text-decoration: none;
		}
	}
	
	h2 {
		font-size: 1.5rem;
		font-weight: $fontWeightThick;
		margin: ($lineHeight * 2rem) auto;
		page-break-after: avoid;
		text-align: center;
		a:link,
		a:visited,
		a:hover,
		a:active {
			color: $colorText;
			text-decoration: none;
		}
	}
	
	h3,
	h4,
	h5,
	h6 {
		font-size: 1rem;
		font-weight: $fontWeightThick;
		margin: 0 auto;
		page-break-after: avoid;
		text-align: left;
		a:link,
		a:visited,
		a:hover,
		a:active {
			color: $colorText;
			text-decoration: none;
		}
	}
	
	li {
		font-weight: $fontWeightThin;
		a:link,
		a:visited,
		a:hover,
		a:active {
			color: $colorPrimary;
			font-weight: $fontWeightThick;
			text-decoration: none;
			@media print {
				color: $colorText;
				font-weight: $fontWeightThin;
			}
		}
		a:visited {
			color: $colorSecondary;
			@media print {
				color: $colorText;
			}
		}
	}
	
	ol {
		list-style: decimal inside;
		margin: 0 auto ($lineHeight + rem);
		padding: 0;
		page-break-inside: avoid;
	}
	
	p {
		font-weight: $fontWeightThin;
		margin: 0 auto ($lineHeight + rem);
		text-align: left;
		a:link,
		a:visited,
		a:hover,
		a:active {
			color: $colorPrimary;
			font-weight: $fontWeightThick;
			text-decoration: none;
			@media print {
				color: $colorText;
				font-weight: $fontWeightThin;
			}
		}
		a:visited {
			color: $colorSecondary;
			@media print {
				color: $colorText;
			}
		}
		a[href]:after {
			@media print {
				content: " (" attr(href) ")";
			}
		}
	}
	
	sub {
		font-size: 75%;
		position: relative;
		top: 0.25rem;
		vertical-align: baseline;
	}
	
	sup {
		font-size: 75%;
		position: relative;
		top: -0.375rem;
		vertical-align: baseline;
	}
	
	ul {
		list-style: circle inside;
		margin: 0 auto ($lineHeight + rem);
		padding: 0;
		page-break-inside: avoid;
	}
	
	
	/*
			TYPOGRAPHIC CONTAINERS
	*/
	blockquote,
	pre {
		background-color: $colorContainer;
		margin: 0 auto ($lineHeight + rem);
		padding: ($lineHeight + rem) 1rem ($lineHeight + rem);
		:last-child {
			margin-bottom: 0;
		}
	}
	
	
	/*
			ELEMENTS
	*/
	*,
	*:before,
	*:after {
		box-sizing: inherit;
	}
	
	html {
		background-color: $colorBackground;
		box-sizing: border-box;
		color: $colorText;
	}
	
	body {
		margin: 0;
		overflow-wrap: break-word;
		-webkit-text-size-adjust: 100%;
		-ms-text-size-adjust: 100%;
	}
	
	
	/*
			MEDIA
	*/
	figure {
		margin: 0 auto ($lineHeight + rem);
		padding: 0;
		page-break-inside: avoid;
		width: 100%;
		figcaption {
			font-size: 0.75rem;
			text-align: center;
		}
		img {
			margin-bottom: 0;
		}
		&.halfLeft {
			float: left;
			margin-bottom: 0;
			margin-right: 8px;
			width: 50%
		}
		&.halfRight {
			float: right;
			margin-bottom: 0;
			margin-left: 8px;
			width: 50%;
		}
		&.quarterLeft {
			float: left;
			margin-bottom: 0;
			margin-right: 8px;
			width: 25%;
		}
		&.quarterRight {
			float: right;
			margin-bottom: 0;
			margin-left: 8px;
			width: 25%;
		}
	}
	
	img {
		display: block;
		margin: 0 auto;
		padding: 0;
		page-break-inside: avoid;
		width: 100%;
	}
	
	video {
		display: block;
		margin: 0 auto;
		padding: 0;
		page-break-inside: avoid;
		width: 100%;
		&.half {
			width: 50%;
		}
	}
