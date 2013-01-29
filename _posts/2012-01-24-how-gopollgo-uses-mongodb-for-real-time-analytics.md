---
layout: post
title: "How GoPollGo Uses MongoDB for Real-Time Analytics"
---
I wrote a post on the official GoPollGo blog about [Migrating to MongoDB](http://gopollgo.com/blog/gopollgo-is-now-mongodb)

tl;dr: MongoDB allows us to do fast real-time increments on a large number of dynamic analytics attributes. Its flexibility improved our code iteration speed as well. We don't do any complex relational queries across polls, so switching 100% of our persistence layer from MySQL to MongoDB worked great.