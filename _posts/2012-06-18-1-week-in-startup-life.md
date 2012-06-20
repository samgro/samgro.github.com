---
layout: post
title: A Week in Startup Life
description: My favorite part about working at a 3 person startup is that in any given week, I get to work on different challenges across the entire web development stack from server infrastructure to CSS. Here's a snapshot of last week.
---
My favorite part about working at a 3 person startup ([GoPollGo](http://gopollgo.com/)) is that in any given week, I get to work on different challenges across the entire web development stack from server infrastructure to CSS. Here's a snapshot of last week.

## Monday
Worked with [Ben](http://twitter.com/bensign) and [Paul](http://twitter.com/kompfner) to fix front-end bugs from the redesign of our mobile site, which we launched the previous Friday.

## Tuesday
Worked with Ben on improving our page load times to increase our servers' requests per second by optimizing some database queries, rewriting our JSON serialization to be more efficient in Ruby, and eliminating data unnecessary for the initial page load. By 10pm, we achieved a tenfold increase in requests per second from the beginning of the day.

## Wednesday
Worked on visually polishing the mobile site and fixing the remaining bugs. [Launched with Twitter Expanded Tweets](http://gopollgo.com/blog/announcing-our-partnership-with-twitter) after 9 months of business development. Celebrated with Ben and Paul over beers at the [Nuthouse](http://www.yelp.com/biz/antonios-nut-house-palo-alto).

## Thursday
We've been hit by a spammer. Declared war on Viagra related polls. Researched spam filtering to develop a plan. Decided to try using a [reverse CAPTCHA](http://lesseverything.com/blog/archives/2008/10/08/less-reverse-captcha/) as a first line of defense. Developed an improved admin interface for moderating polls.

## Friday
Developed a honeypot to filter spam, where we add `display: none` to the first option's `<input>` and ensure that it's left blank. It worked! Got [featured on Mashable for Expanded Tweets integration](http://mashable.com/2012/06/15/gopollgo/).

## Saturday
While eating brunch, got a message from Ben that someone had exploited a Javascript injection on our site. The exploit was non-malicious and Ben had plugged the hole by the time I got to my computer. Upon further investigation, I discovered the root cause of the bug appeared to be a vulnerability in an open source project we use. Emailed the project maintainer. Details to follow once it has been patched.
