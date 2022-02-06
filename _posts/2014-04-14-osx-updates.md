---
title: "Xcode 5.1, iOS 7.1 and OS X 10.9 for Mac and iOS builds"
created_at: Tue 15 Apr 2014 8 PM UTC
author: Henrik Hodne
twitter: henrikhodne
layout: post
permalink: 2014-04-15-xcode-51-ios-71-osx-109
---

We are happy to announce that Xcode 5.1, iOS 7.1 and OS X 10.9 support is coming
to Travis CI! We will be updating travis-ci.org this Wednesday, [April 16th at 3
PM UTC][org-time] and travis-ci.com Friday, [April 18th at 3 PM UTC][com-time].

[org-time]: http://www.timeanddate.com/worldclock/fixedtime.html?iso=20140416T15
[com-time]: http://www.timeanddate.com/worldclock/fixedtime.html?iso=20140418T15

We've also updated the installed Homebrew packages, so the following versions
are now preinstalled:

* xctool version 0.1.15
* RubyMotion verison 2.26
* [nomad-cli](http://nomad-cli.com)

With this update we've also removed some older versions of iOS SDKs, the
available SDKs are now iOS 6.1, 7.0 and 7.1.

We've also switched the default Ruby over to Ruby 2.0.0 to match the system Ruby
on OS X 10.9. Note that this Ruby verison is installed with RVM, so there is no
need to use `sudo` to install gems.

If you see any issues after the update, please [let us
know](mailto:support@travis-ci.org) or [open a
ticket](https://github.com/travis-ci/travis-ci/issues).

