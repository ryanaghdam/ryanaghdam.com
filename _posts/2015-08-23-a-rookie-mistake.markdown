---
title: "A Rookie Mistake: ryanaghdam.com Re-written"
date: 2015-08-23
category: software
layout: post
excerpt: I spent, or wasted, the weekend rewriting the backend for ryanaghdam.com
---

Frustrated with building my website with [Jekyll][0] and [Liquid Templates][1], I decided that I could write myself something to take its place.  I ignored the many available solutions and started thinking of waht I wanted in a blogging platform.

1. I wanted to store posts as plain markdown files.  A web interface was not only unnecessary but unwanted.

2. Since I was writing it myself, I wanted to use node.js and try out some modules: [Ramda][2], [proxyquire][3], and [tape][4].

3. I wanted the content to be completely separate from the presentation layer and easily portable, for when I inevitably want to spent a weekend re-writing code rather than content.

4. I wanted to continue to use the [Lightbox][5] plugin.  I was unhappy that I was using a [Liquid template include][6] to insert images.  I wanted to be able to just include an image using the traditional Markdown syntax.

5. I also wanted to run the site with very minimal cost.

Half a Saturday and most of a Sunday later, let's see what I have.

## Content Package

A package, [`ryanaghdam-content`][7], provides an API to read all posts, read one post (matching by slug), or all posts from a given category.

A [script][8] runs during install time to resize the source images using ImageMagick.

The images are [surfaced on the presentation layer][9], using [Express's static file middleware][10].

Most functions are memoized so that filesystem access is cached.  For the most part, this package adheres to basic functional programming practices; most functions are [pure][11].

## The Presentation layer

The front end is a simple Express application, [`ryanaghdam-homepage`][12].

Controllers access the API exposed by the `ryanaghdam-content` package and render [Jade][13] templates.

A [content service][14] is used to slightly transform data before it's sent off to Jade.  This could have -- and possibly should have -- been done in the content package.  I chose to do the transformation here, because I want to use it as an example for how something at work can be done.

Unlike `ryanaghdam-content`, the Express application is not covered by tests.  I plan on using [Nightwatch][15] or [Nemo][16].

## The Aftermath

I mentioned a few goals that I wanted to accomplish.

1. Store content in plain markdown files -- success.  All content is plain markdown with YAML front matter.  It's easily portable for when I next change my mind.

2. Use Ramda, proxyquire, and tape -- success.

3. Separate the content from the presentation layer -- success.  The content is a separate, published npm package.  A completely different presentation layer can use the same content.  There is, however, a problem with this approach.  To make a content change, I must: update and publish the content package, update [`ryanaghdam-homepage`][17] to use the latest version of the content package, and then deploy to Heroku.  Previously, with my Jekyll-based setup, I just had to push my content to GitHub.  [Travis-CI][18] would automatically run to build and deploy (to [GitHub Pages][19]).

4.  Use Lightbox with plain Markdown -- success.  I am using [markdown-it][20] to render Markdown.  It features a plugin interface, which enabled me to write a custom plugin that changed the way images are rendered.  It's pretty [poorly written][21].

5. Minimal runnings costs -- TBD.  I am currently using a free-tier [Heroku][22] instance.  Time will tell if that's a viable solution.

Not too bad when looking at just the goals.  But is it any better?  I have a more complex deployment process, a more complex hosting environment,  and a website that, to the user, hasn't changed a bit.

I got to spend some time working on a project that uses some modules and architecture that I wanted to try.  Is the product -- my website -- noticeably improved, or even different?

I think this is a common rookie-mistake -- rewriting something just to use new technology and certainly something I should have been more cognizant of.  If it were a professional project, rather than a rainy weekend project, it would have been an tremendous waste of time and effort.

It's a good thing that I enjoy writing things that nobody reads -- these blog posts and software -- otherwise this weekend would have been a waste.

[0]: http://jekyllrb.com/
[1]: http://liquidmarkup.org/
[2]: http://ramdajs.com/
[3]: https://github.com/thlorenz/proxyquire
[4]: https://github.com/substack/tape
[5]: http://lokeshdhakar.com/projects/lightbox2/
[6]: https://github.com/ryanaghdam/ryanaghdam.github.io/blob/3463115dc787445aef90bf544c7f647b1b730d59/_includes/image.html
[7]: https://www.npmjs.com/package/ryanaghdam-content
[8]: https://github.com/ryanaghdam/ryanaghdam-content/blob/v1.0.1/scripts/resize-images.sh
[9]: https://github.com/ryanaghdam/ryanaghdam-homepage/blob/v1.2.0/index.js#L13-L15
[10]: http://expressjs.com/starter/static-files.html
[11]: https://en.wikipedia.org/wiki/Pure_function
[12]: https://github.com/ryanaghdam/ryanaghdam-homepage
[13]: http://jade-lang.com/
[14]: https://github.com/ryanaghdam/ryanaghdam-homepage/blob/v1.2.0/services/content.js#L7-L28
[15]: http://nightwatchjs.org/
[16]: https://github.com/paypal/nemo
[17]: https://github.com/ryanaghdam/ryanaghdam-homepage
[18]: https://travis-ci.org/
[19]: https://pages.github.com/
[20]: https://github.com/markdown-it/markdown-it
[21]: https://github.com/ryanaghdam/ryanaghdam-content/blob/master/lib/domain.js#L3-L34
[22]: http://heroku.com/
