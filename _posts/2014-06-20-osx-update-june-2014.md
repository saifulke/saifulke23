---
title: OS X Update June 2014
layout: post
author: Henrik Hodne
twitter: henrikhodne
created_at: Tue 20 Jun 2014 13:45:00 CEST
permalink: 2014-06-20-osx-update-june-2014
---

It's time for another update to our OS X build environment. This update brings Xcode 5.1.1, RubyMotion 2.29, xctool 0.1.16 and more.

The update is going to be live in the next few days on both travis-ci.org and travis-ci.com.

## New tools

We've installed the following new tools:

- CMake 2.8.12.2 (GitHub issue #[2408](https://github.com/travis-ci/travis-ci/issues/2408))
- GCC 4.8 (available as `gcc-4.8`, `gcc` is still Apple's LLVM-gcc) (GitHub issue #[2423](https://github.com/travis-ci/travis-ci/issues/2423))
- appledoc 2.2 (this used to be installed, but was gone for a little while due to compilation issues) (GitHub issue #[2183](https://github.com/travis-ci/travis-ci/issues/2183))
- xcpretty 0.1.6 (GitHub issue #[2168](https://github.com/travis-ci/travis-ci/issues/2168))
- XQuartz 2.7.6 (GitHub issue #[2351](https://github.com/travis-ci/travis-ci/issues/2351))
- oclint 0.7 (GitHub issue #[1475](https://github.com/travis-ci/travis-ci/issues/1475))
- Appium 1.1.0 (GitHub issue #[2348](https://github.com/travis-ci/travis-ci/issues/2348))

## Updated versions

We've also updated the versions of several tools:

- Xcode 5.1.1 (GitHub issue #[2302](https://github.com/travis-ci/travis-ci/issues/2302))
- CocoaPods 0.33.1
- xctool 0.1.16
- RubyMotion 2.29
- Go 1.2.2
- node 0.10.28
- npm 1.4.15
- RVM 1.25.27
- Ruby 2.1.2 (2.0.0 is still the default)

As always, if you have any issues, shoot us [an email](mailto:support@travis-ci.com).
