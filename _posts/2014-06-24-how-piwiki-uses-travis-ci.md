---
title: How Piwik uses Travis CI to deliver a reliable analytics platform to the community
author: Matthieu Aubry
twitter: matthieuaubry
layout: post
created_at: Tue 24 Jun 2014 14:00:00 CEST
permalink: 2014-06-24-how-piwik-uses-travis-ci
---
![](/images/piwik_app.jpg)

> This post was originally [published on the Piwik
> blog](http://piwik.org/blog/2014/05/piwik-use-travis-ci-ship-analytics-platform-works/).
> The Piwik team kindly gave us permission to repost it here, and we'd like to
> thank them for writing and sharing it! -- Mathias Meyer

In this post, we will explain how the Piwik project uses continuous integration
to deliver a quality software platform to dozens of thousands of users
worldwide. Read this post if you are interested in Piwik project, Quality
Assurance or Automated testing.

### Why do we care about tests?

Continuous Integration brings us agility and peace of mind. From the very
[beginning](http://piwik.org/history/) of the Piwik project, it was clear to us
that writing and maintaining automated tests was a necessity, in order to create
a successful open source software platform.

Over the years we have invested a lot of time into writing and maintaining our
tests suites. This work has paid off in so many ways! Piwik platform has fewer
bugs, fewer regressions, and we are able to release new minor and major versions
frequently.

### Which parts of Piwik software are automatically tested?

* **Piwik back-end in PHP5:** we use PHPUnit to write and run our PHP tests: unit
tests, integration tests, and plugin tests.
* **piwik.js Tracker:** the JS tracker is included into all websites that use Piwik.
For this reason, it is critical that piwik.js [JavaScript
tracker](http://developer.piwik.org/api-reference/tracking-javascript) always works
without any issue or regression. Our Javascript Tracker tests includes both unit
and integration tests.
* **Piwik front-end:** more recently we’ve started to write JavaScript tests for the
user interface partially written in AngularJS.
* **Piwik front-end screenshots tests**: after each change to Piwik, more than 150
different screenshots are automatically taken. For example, we take screenshots
of each of the 8-step installation process, we take screenshots of the password
reset workflow, etc. Each of these screenshot is then compared pixel by pixel,
with the “expected” screenshot, and we can automatically detect whether the last
code change has introduced an undesired visual change. Learn more about [Piwik
screenshot
tests](http://piwik.org/blog/2013/10/our-latest-improvement-to-qa-screenshot-testing/).

### How often do we run the tests?

The tests are executed by [Travis CI](https://travis-ci.org/piwik/piwik) after each change to the Piwik source code.
On average all our tests run 20 times per day. Whenever a Piwik developer pushes
some code to GitHub, or when a community member issues a [pull request](http://developer.piwik.org/guides/contributing-to-piwik-core), Travis CI
automatically runs the tests. In case some of the automated tests started
failing after a change, the developer that has made the change is notified by
email.

### Should I use Travis CI?

Over the last six years, we have used various Continuous Integration servers
such as Bamboo, Hudson, Jenkins… and have found that the Travis CI is the ideal
continuous integration service for open source projects that are hosted on
Github. Travis CI is free for open source projects and the Travis CI team is
very friendly and reactive! If you work on commercial closed source software,
you may also use Travis by signing up to [Travis CI Pro](https://travis-ci.com).

### Summary

Tests make the Piwik analytics platform better. Writing tests make Piwik
contributors better developers. We save a lot of time and effort, and we are not
afraid of change!

Here is the current status of our builds:

Main build: [![](https://travis-ci.org/piwik/piwik.svg?branch=master)](https://travis-ci.org/piwik/piwik)

Screenshot tests build: [![](https://travis-ci.org/piwik/piwik-ui-tests.svg?branch=master)](https://travis-ci.org/piwik/piwik-ui-tests)

PS: If you are a developer looking for a challenge, [Piwik is hiring a software
developer](http://piwik.org/blog/2014/05/piwik-expanding-seeking-talented-software-engineer-new-zealand-poland/) to join our engineering team in New Zealand or Poland.
