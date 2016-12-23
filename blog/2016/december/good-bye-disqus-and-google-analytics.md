<!--
Title: Good-bye Disqus and Google Analytics
Author: Jacob Moen
Date: 2016/12/24 00:53
Datetime: 2016-12-24
Description: For privacy and security reasons I removed Google Analytics tracking and Disqus from my sites 
View: post
ogimage: donottrack/do_not_track_mobile.jpg
thumb: donottrack/do_not_track_custom.jpg
Keywords: privacy, disqus, google analytics, analytics, google, security
Tags: privacy
blogpost: true
published: false
-->
(lightbox:Do Not Track - Photo by pippalou at Morguefile.com  source:donottrack/do_not_track_mobile.jpg target:donottrack/do_not_track.jpg)
It seems like - and is actually true as well! that we are tracked where ever we go these days.

So, I thought to myself: do my sites really have to track you as well?

I don't want to track, or help to track, anyone.

(clearfix:)

Additionally, in the European Union, we are required by law to comply with the [Cookie Directive](http://ec.europa.eu/ipg/basics/legal/cookies/index_en.htm), which basically means that we need to at least inform our visitors that we are collecting cookies and link to a privacy policy page explaining what cookies are, and whatnot.

So, I have decided to get rid of Google Analytics and Disqus from my sites.

That should mean that my sites are not helping tracking anyone, and that the all the EU cookie regulation sheenanigans is avoided. Win-win!

## Google Analytics ##
Like so many other, I have been (blindly) adding Google Analytics to my sites.

Thinking about it, it is not really useful to me, since I don't monetise my site and haven't got that many visitors anyway :p

I save the request to the Google servers, and avoid setting a tracking cookie.

So, I switched to a simple Google Site Verification code that does nothing but verify site ownership.

## Disqus ##
I have been meaning to ditch Disqus for a long, long time.

I want to own the data myself, my comments.

I do not want to aid Disqus in tracking people. They were collecting information about my visitors so that they could serve targeted ads, 'community' suggestions, etc.

Disqus is a so-called 'free' service, but what we are really paying them with is information.

So, I downloaded my data and deleted my sites.

## Self-hosted comments ##
I am now using [HashOver 2.0](https://github.com/jacobwb/hashover-next) PHP comment system.

(inimage: Cookie Monster not happy source:donottrack/cookie_monster.jpg align:right)

I wrote a script that imported my comments from Disqus, and they are now stored safely on my server.

Any email addresses are encrypted so in the highly unlikely event that someone manages to compromise the data, they won't be able to steal any personal information, because they don't have the encryption key.

## You are welcome ##

I hope that you will appreciate not being tracked :)

And everyone, except the cookie monster, will be pleased to know that this site is absolutely cookie-free!

(clearfix:)
