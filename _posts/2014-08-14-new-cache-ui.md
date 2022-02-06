---
title: "New Cache UI"
created_at: Thu 14 Aug 2014 18:00:00 CET
author: Konstantin Haase
twitter: konstantinhaase
layout: post
permalink: 2014-08-14-new-cache-ui
---

Installing external dependencies on every build can take quite some time. This is why at the end of last year we introduced [dependency caching](/2013-12-05-speed-up-your-builds-cache-your-dependencies). Since then, we have kept on improving the feature, most recently launching [Mac support](/2014-07-31-caching-all-the-things-on-the-mac-platform).

## Clearing Caches

Sometimes your cache gets stale and contains files that will cause your build to fail. For instance, a cache may be invalidated by [build environment updates](/2014-07-24-upcoming-build-environment-updates) if the cache contains compiled code. It might well be that the only solution is to get rid of the old cache.

<figure>
  [ ![travis cache --delete](http://docs.travis-ci.com/images/cli-cache.png) ](http://docs.travis-ci.com/images/cli-cache.png)
  <figcaption>Running <tt>travis cache --delete</tt> inside the project directory.</figcaption>
</figure>

To make it possible for you to get an overview over your caches and delete them if need be, we added the [`cache` command](https://github.com/travis-ci/travis.rb#cache) to our command line client at launch.

## New UI

We are happy to announce a new view inside our web UI. Like the command line client, it allows you to view which caches exist and clear out a single cache, all caches for one branch, or all caches all at once.

<figure>
  [ ![New Caches UI](https://api.monosnap.com/image/download?id=Umct4Y3ZceLv8xw4RNqhsFDNBoRL09) ](https://api.monosnap.com/image/download?id=Umct4Y3ZceLv8xw4RNqhsFDNBoRL09)
  <figcaption>Viewing caches for a repository</figcaption>
</figure>

To get to the cache view, navigate to any project on [Travis Pro](https://travis-ci.com/) and you should find a "Caches" link in the cog menu.

## Cache fallback

Please keep in mind: If you delete the cache for a branch other than master, the next build on that branch will fall back to the master cache instead of using an empty cache. This is important if the master branch cache is causing issues, too.
