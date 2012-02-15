---
layout: post
title: Clear, a checklist app, just raised the bar for mobile design
---

**tl;dr** Clear is a simple, beautiful new checklist app. If you have an iPhone and use it or want to use it for grocery lists, todo lists, etc., or if you work on mobile apps and are looking for design inspiration, drop what you're doing and <a href='http://itunes.apple.com/us/app/clear/id493136154?mt=8' target='_blank'>download Clear from the App Store</a>.

<img src='/images/clear-lists.png' alt='Clear lists' width='144' height='216' class='left' />

Every programmer makes a checklist app/website at some point in their life. Everyone uses checklists, everyone uses checklists differently, and they seem easy enough to make your own that it's easy to try. Given the plethora of apps for this purpose, I didn't imagine it possible for a checklist app design to be so innovative that it raises the bar for all mobile app design. <a href="http://www.realmacsoftware.com/clear/" target='_blank'>Clear</a> did just that.

I use checklists a lot. Grocery list. Todo list. Movies I want to watch. I've had a surprising struggle finding a good iPhone app for these purposes. My requirements are minimal:

1. Easy drag and drop to reorder.
1. Easy to add many items quickly.
1. Easy to clear completed items.
1. (Bonus) Sync to web

That's it. I literally couldn't find this app. <a href="http://www.getflow.com/" target='_blank'>Flow</a> packed a bunch of features I didn't need and charged $9/month. <a href="http://itunes.apple.com/us/app/lists/id423591440?mt=8" target="_blank">Lists</a> didn't have a way to clear completed items and kept a badge notification counting the number of incomplete items in the app (WTF?). Other apps, like the native Reminders, don't have a way to reorder items (at least as far as I can tell). For me, a checklist app doesn't need any of the following popular features:

* Social integration
* Email integration
* Due dates
* Comments
* Long form "details"
* Subitems
* Integration with Pivotal Tracker
* Integration with MS-DOS

OK, I made up the last one. You got me. The point is - everyone who makes a checklist app either does it as a crappy throwaway project, or thinks it's going to be The Next Great Thing and spends so much time building cool features for 1% of their potential users that they don't build a good interface for the checklist itself, the core feature.

I had actually given up on finding this app and started building my own. This made me realize that is trivial as it seems, designing a good checklist on a mobile phone is actually hard. Here are a few of the design challenges I've encountered:

* How do you decide whether to add items to the top or bottom of the list?
* What if you want to add an item in the middle?
* How do you arrange the buttons for "Add", "Edit", and "Clear completed" without making the app hideous and/or unusable?
* Should tapping an item's text start editing, or check the item?
* How do you add lots of items quickly?

Clear thought outside the box, ditched every piece of iOS boilerplate chrome, and used gestures to brilliantly solve all of these problems. One of the problems with gestures is that they're hard to learn. A checklist app, however, can populate its initial list with short tips teaching you all the gestures! This isn't unique to Clear, but it works really well for them. Here are the gestures they used to solve the problems above:

<p><center><img src='/images/clear-gesture.png' alt='Screenshot: Pull down to add an item' width='320' height='480' /></center></p>

* Tapping the space at the bottom of a list adds a new item to the bottom. A soft swipe down (i.e. pulling the list down to allow space for a new item) adds a new item to the top.
* Pinching two items apart adds an item in between - so obvious once you realize it. I'm just not sure anyone realized that until Clear.
* There is no edit mode. No checkbox. Swipe right to complete an item, left to delete. Hold down to drag and reorder. Swipe up to clear completed items.
* To add lots of items quickly, swipe down in the area above the keyboard to complete the current item and add another.

<p><center><img src='/images/clear-edit.png' alt='Screenshot: editing/adding items' width='320' height='480' /></center></p>

Clear also reclaimed screen real estate by replacing the traditional navigation bar/back button with two gestures to go back - pinch vertically inward, and swipe quickly up. I personally prefer swipe quickly up.

There are a few quirks I'd love to see Clear fix in the next release:

* A synced web interface so I can edit my lists from my computer.
* I usually swipe down from the top of the list to add an item to the top, which seems metaphorically correct to me (even though the gesture works on any part of the screen). However, this pulls down the iOS notification center. Not sure the best way to fix this.
* For quick add, swiping down to add an item above works great, but swiping up should add the new item below.
* Once you fill the screen, there's nowhere to tap to add an item to the bottom of the list. They should just add a black dummy row here.
* Sometimes when I try to move up the list hierarchy with a fast swipe, I end up creating a new item (small swipe). They might just need to tweak the velocity boundary between these two gestures.
* There is no undo. You should be able to shake to undo.

I hope the Clear gestures become conventional for list editing. Clear raised the bar for all mobile apps, not just checklists. Every mobile designer should be thinking - how can I remove features, remove buttons, and take advantage of the unique properties of a handheld device? How can I take the mundane and make it simple, elegant, beautiful?
