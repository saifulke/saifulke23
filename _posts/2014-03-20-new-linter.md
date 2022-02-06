---
title: Validate your .travis.yml, with Super Powers
created_at: Thu 20 Mar 2014 18:17:48 CET
author: Konstantin Haase
twitter: konstantinhaase
layout: post
permalink: 2014-03-20-validate-travis-yml-configuration-with-super-powers
---

Users wonder why their build doesn't start, but often the culprit is `.travis.yml`. We introduced [our web linter](http://lint.travis-ci.org/) as tool to validate a `.travis.yml`. Until recently, this solution was far from ideal. Most settings were simply ignored, and those that were validated often resulted in false positives. This tool wasn't all that useful.

We have now replaced it with a complete rewrite. It is using our brand new [travis-yaml](https://github.com/travis-ci/travis-yaml) gem. This means instead of being very rudimentary and not well maintained, it is powerful and descriptive when it comes to spotting issues in your [build configuration](http://docs.travis-ci.com/user/build-configuration/).

![](/images/weblint.png)

You can also use this tool to check your [repository directly](http://lint.travis-ci.org/sinatra/sinatra) (including [branches](http://lint.travis-ci.org/sinatra/sinatra?branch=1.2.x)), and [gists](http://lint.travis-ci.org/gist/9639067) directly.

### Future Plans

Having a new linter was just a byproduct of creating the [travis-yaml](https://github.com/travis-ci/travis-yaml) library. We plan to use this small gem throughout our system. That way we will have one central definition for the `.travis.yml` format.

First, we need to get 100% coverage of the currently supported configuration options, though.

Why don't you give [the new linter](http://lint.travis-ci.org/) a try and tell us what you think?