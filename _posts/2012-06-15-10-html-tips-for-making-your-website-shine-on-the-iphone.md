---
layout: post
title: "10 HTML/CSS Tips for Making your Website Shine on the iPhone"
---
When the iPhone was released in 2007, Mobile Safari was optimized to display the websites of the day, which had no mobile user interface optimizations. Today, it is increasingly common to develop either a separate mobile website or a responsive site design that is specific to mobile. There are a number of quirks that a modern front-end developer/designer will likely run into when testing their site on the iPhone. Fortunately, there are a number of webkit vendor prefixes, custom tags and optimizations that can make your website shine on the iPhone.

## 1. Move Javascript to the end of the body
If you do one optimization for mobile, take this one. Mobile devices tend to have extremely limited bandwidth compared to the wireless connection you're likely working from on your development machine. Nothing gets rendered on the page until the `<head>` content, including CSS and Javascript, gets downloaded. If you have a Javascript-intensive app, this 100kb or so file could take 5-10 seconds to download. When I tap through a link to your site from Twitter, if the page is still a blank white canvas after 5 seconds, I hit the back button.

A little bit of upfront planning can help prevent this situation. Even the most intensive Javascript app can show the user something with plain HTML and CSS, even if it's just a logo and an animated loading GIF. The animated loading GIF below tells the user to stick around, hopefully buying a few more seconds before the user hits the back button.

An aside on download performance: every HTTP request is particularly precious on mobile. Desktop best practices for performance are even more important. Make sure your assets are concatenated, minified, and served from a CDN with GZip. [GZipWTF.com](http://gzipwtf.com/) is a great site for testing this. Common images should be served from a sprite or data url - both of these are easy to do with [Compass](http://compass-style.org/).

## 2. Sizing and zooming
Mobile Safari was originally designed to display non-mobile optimized websites, so if you don't declare a viewport in the head of your document, Safari will display the entire page zoomed out. To fix this, add the following to your head:

    <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no" />

This tells the mobile browser to set the initial width of the browser window to the width of the device so the website is constrained to vertical scrolling. The `maximum-scale` and `user-scalable` properties are not required and some sources will tell you to leave these on so that the user can zoom in, but it is pretty standard to turn these off and can save some design headaches.

When rotating from portrait to landscape, Mobile Safari seems to adjust font-sizes at random. I can't tell any rhyme or reason to how it does this, but adding `-webkit-text-size-adjust: none;` to your body CSS will save you from this headache.

## 3. Box sizing
Congratulations! You probably aren't designing for IE7 on your mobile site. That means you are no longer beholden to the traditional box model, where `width` and `height` properties do not include borders and padding. Setting `box-sizing: border-box` allows set `width 100%` on any element with padding and border - this is particularly useful in mobile design, where you commonly want an input or other element to take up 100% of the parent's width but include a border and padding. This trick will save you from creating unnecessary extra container elements and other unpleasant hacks. Add this to the top of your CSS:

    * {
      -webkit-box-sizing: border-box;
      -moz-box-sizing: border-box;
      box-sizing: border-box;
    }

or, in compass:

    @import "compass/css3";
    * {
      @include box-sizing(border-box);
    }

[Paul Irish explains this](http://paulirish.com/2012/box-sizing-border-box-ftw/) more thoroughly.

## 4. Form styling
Webkit adds some styling elements to form elements by default, such as a dark box shadow on the top of `input` and `textarea`. If you want to design your own custom input elements, you'll need to add this to your CSS:

    input[type="password"],
    input[type="datetime"],
    input[type="datetime-local"],
    input[type="date"],
    input[type="email"],
    input[type="month"],
    input[type="number"],
    input[type="tel"],
    input[type="text"],
    input[type="time"],
    input[type="week"],
    input[type="url"],
    textarea {
      -webkit-appearance: none;
    }

![Webkit form styling - before and after](https://img.skitch.com/20120616-ning5wyhapxf88etg4xx68wi1b.jpg)

## 5. Tap and hold link popup dialog
When you tap and hold on a link on the iPhone, a modal dialog pops up allowing you to open the link in a new tab or copy/paste it. This doesn't make sense for many links in a Javascript app, which are internal actions. For each of these links, you'll need to add `-webkit-touch-callout: none`.

![Touch callout dialog](https://img.skitch.com/20120616-j8qy52y2sgqk36wht5dnssdfmj.jpg)

## 6. Tap effects
Mobile Safari automatically adds a gray, semi-transparent highlight over links when tapped. This is a helpful user experience since it allows the user to see that they've clicked something actionable. In general, it's a good idea to keep these around since the user expects them and the effects are more reliable than the `:hover`, `:focus` and `:active` pseudo-selector styles. For example, these effects don't go away when the user pulls their finger outside the clickable region, which is valuable feedback.

Unfortunately, Mobile Safari sets tap highlights not only on links, but also on any element with a Javascript event listener on 'click'. This has side effects when using event delegation. Event delegation (binding an event to a single common parent element instead of binding lots of identical events to lots of children) is a common Javascript pattern to improve performance. If you're using [jQuery.on()](http://api.jquery.com/on/) or [Backbone.js events](http://backbonejs.org/#View-delegateEvents), your site likely uses this pattern.  Mobile Safari adds a tap highlight to the parent element with the delegated event. This means tapping a non-clickable child will cause the entire region to highlight, and text selection will be disabled. Presumably Apple made this decision to compensate for the common anti-pattern of handling important click actions on non-`<a>` tags, but it comes with the cost of punishing developers using good Javascript practice. For accessibility and semantic reasons, all clickable items on your page should be in `<a>` tags. To reset the tap highlight to the correct behavior (tap highlight on links and only on links), add the following global styles:

    /* Disable webkit tap-highlighting on non-links */
    body {
      -webkit-tap-highlight-color: rgba(0,0,0,0);
    	tap-highlight-color: rgba(0,0,0,0);
    }

    /* Enable webkit tap-highlighting on links */
    a {
      -webkit-tap-highlight-color: #999;
      tap-highlight-color: #999;
    }

In addition to the tap highlight, you might want other custom effects on elements such as buttons, i.e. a 'pressed' state. By default, however, Mobile Safari ignores the `:hover`, `:focus` and `:active` pseudo-selector styles. To enable them, you just need an event listener on `'touchstart'`:

    document.addEventListener("touchstart", emptyFunction, false)

## 7. Media queries for retina images
Retina iPhones and iPads display page elements at double scale - a 16x16 icon is scaled up to 32x32. That's 4 times more pixels than a non-retina iPhone in the same amount of space. Most 16x16 icons look pretty bad when scaled up to 32x32, so you'll need to add an enhanced version of your resources to target with a media query and resize with the `background-size` property. We use the Compass `inline-image` mixin to minimize our HTTP request overhead and serve the icons directly as data in our CSS. Here's what that looks like in Compass:

    .my-icon {
      height: 16px;
      width: 16px;
      background: inline-image('mobile/my-icon.png');
    }

    @media screen and (-webkit-min-device-pixel-ratio: 2) {
      .alerts-icon {
        background: inline-image('mobile_2x/my-icon.png');
        background-size: 16px 16px; 
      }
    }

## 8. Use CSS3 transitions instead of JS animations when possible
CSS3 transitions are hardware optimized in Mobile Safari. Take advantage of this whenever possible. Javascript animations (such as those provided by `jQuery.animate()`) often work well but sometimes can appear a bit choppy.
Libraries such as [Modernizr](http://modernizr.com/) provide detection of available CSS features.

## 9. Avoid fixed positioning
Apple didn't implement `position: fixed` until iOS 5. It still seems a little rough around the edges, with unexpected and sometimes unsightly things happening upon opening the keyboard or scrolling. Avoiding fixed positioning will make both you and your users happy.

## 10. Provide an icon for the home screen
If a user adds you to their bookmarks or home screen, you'll want your own custom icon, which is much bigger than a traditional favicon. You'll want a 144x144 image so it looks good on Retina display iPad, referenced in your `<head>` like this:

    <link rel="apple-touch-icon" href="/my-icon.png" />

## Bonus: all together now
A lot of this is boilerplate that should not require being rewritten for every project. I've written a compass extension, [mobile_reset](https://github.com/samgro/mobile_reset), to quickly add the CSS for most of the issues discussed here. If you don't use SASS and Compass, you can just copy and paste the [source stylesheet](https://github.com/samgro/mobile_reset/blob/master/stylesheets/_mobile_reset.scss).
