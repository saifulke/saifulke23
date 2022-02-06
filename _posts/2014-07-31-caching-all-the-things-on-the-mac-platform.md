---
title: Caching (all the things) on the Mac platform
author: Henrik Hodne
twitter: henrikhodne
layout: post
created_at: Thu 31 Jul 2014 17:40:00 CEST
permalink: 2014-07-31-caching-all-the-things-on-the-mac-platform
---

Back in December last year, we [announced][cache-blog-post] dependency caching
for private repositories. Until now this feature has only been available to
builds running on our Linux platform. Today we are enabling this feature for
builds on the Mac platform too (only for private repositories at this time).

You can cache gems installed with Bundler in the same way you would on

You can use Bundler caching just like you would for a build on the Linux
platform:

    cache: bundler

In addition to Bundler caching and directory caching, we also shipped built-in
support for CocoaPods caching. To start using it, add this to your
*.travis.yml*:

    cache: cocoapods

Check out [the documentation][cocoapods-cache-docs] for more information, for
example how to add caching for repositories where the *Podfile* is not in the root
of the repository, or how to use both Bundler and CocoaPods caching.

Caches for Mac and Linux builds are stored in different data centers to optimize
the download and upload speeds. This means that the caches are not shared
between Mac and Linux builds.

[cache-blog-post]: http://blog.travis-ci.com/2013-12-05-speed-up-your-builds-cache-your-dependencies/
[cocoapods-cache-docs]: http://docs.travis-ci.com/user/caching/#CocoaPods
