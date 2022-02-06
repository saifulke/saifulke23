---
title: Build Status Badges now Support SVG
layout: post
created_at: Thu 20 Mar 2014 12:00:00 CET
author: Mathias Meyer
twitter: roidrage
permalink: 2014-03-20-build-status-badges-support-svg/
---
Build status badges for readme files have a long history at Travis CI.
Originally conceived by [Jeff Kreeftmeijer](https://twitter.com/jkreeftmeijer),
they were initially added on [20 February
2011](https://github.com/travis-ci/travis-ci/commit/2b50cc6a86e21bafd37986fb2357a258c941b612).
That's more than three years ago!

Here's what the first ever build status badge looked like:
![](http://s3itch.paperplanes.de/Screenshot_20140320_165453_20140320_165507.jpg)

Now they've become part of the trust chain in a project. The green badge
instills confidence that the project maintainer is not only actively writing
test, but that they're also caring for having the automated build pass.

Since then, the badges have become omnipresent, adopted by a lot of services
like [Code Climate](http://codeclimate.com) and
[Gemnasium](http://gemnasium.com).

They've gotten so popular that a group of fine people huddled together to build
[Shields](http://shields.io), a common endpoint and provider of unified status
badges.

Shields was the driving force behind the unified PNG badges that have been in
use for the past couple of months
(![](https://raw.githubusercontent.com/travis-ci/travis-api/515ffb8a8a881f18c7e27bf134da81a8de54945f/public/images/result/passing.png)), and lately, they've been pushing towards
badges based on SVG. With Retina being everywhere, it was about time that Travis
CI provided better, scalable badges as well.

As of today, badges displayed in Travis CI are based on the SVG version, and our
status image dialog shows them as defaults as well. Here's an example of how
they look, fingers crossed the build is green!

[![](https://travis-ci.org/travis-ci/travis-api.svg?branch=master)](https://travis-ci.org/travis-ci/travis-api)

For the time being, we'll still serve the PNG files on the old URLs, but we'll
eventually serve the SVG version by default for both URLs.

Many thanks to the [Shields](http://shields.io) project for providing us with
these badges and for pushing towards them being unified across all projects
actively using them.
