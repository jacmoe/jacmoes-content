<!--
Title: A lean facelift
Author: Jacob Moen
Date: 2017/10/31 11:53
Datetime: 2017-10-31
Description: M.css is a CSS framework for content-oriented websites and it is perfect for my site.
View: post
ogimage: mcss/facelift.jpg
thumb: mcss/facelift_custom.png
Keywords: css, site, theming, mcss
Tags: site, theming, css
blogpost: true
published: true
-->
(lightbox:Facelift source:mcss/facelift_mobile.png target:mcss/facelift.png)

It is that time of year when I grow tired of the design of my site, and decides to rewrite the theme.

I have been using the excellent, and very lean! CSS (Sass) framework [Bourbon](http://bourbon.io/), with [Neat](https://neat.bourbon.io/) for the grid layout, and while it is lean, I still managed to produce a certain amount of messy Sass code! :p

Partly because I am not yet skilled enough to write truly clean Sass code, but mainly because Bourbon, and Neat, is agnostic to my use case. Which is usually a good thing, but in my case I just need a simple CSS framework tailored for my specific use case, which is pages with content and blog posts.

(clearfix:)

## Enter m.css

(lightbox:m.css source:mcss/mcss_mobile.png align:right target:mcss/mcss.png)

Luckily, I found [m.css](http://mcss.mosra.cz/) which describes itself as follows:

> A no-non­sense, no-JavaScript CSS frame­work and Pel­i­can theme for con­tent-ori­ent­ed web­sites.

Armed with that, I managed to get rid of 95 % of my Sass code, simply because it works beautifully out of the box.

It features a grid, inspired by Bootstrap, sensible typography, buttons, and has a few tricks up the sleeve, like extra support for articles/landing pages and other things that people who write content oriented websites would want.

It does not feature anything else, though, so it is very, very lean.

All in all, a joy to work with! And I highly recommend that you give it a try if you have a site that needs a facelift, and/or have grown tired of increasingly complex CSS frameworks that comes packed with features that you don't need.

Don't get me wrong: Bourbon and Neat is still an excellent choice if you know exactly what you want and how to get it and have needs that goes beyond a simple, yet effective, content oriented site.

But, do check out [m.css](http://mcss.mosra.cz/) - it's great!

Also, it does feature a light theme, if you're not into the dark side of things.

(clearfix:)
