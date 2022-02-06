---
title: Per Repository Concurrency Setting
author: Konstantin Haase
twitter: konstantinhaase
created_at: Friday 18 Jul 2014 16:00:00 CEST
permalink: 2014-07-18-per-repository-concurrency-setting
layout: post
---

<figure class="smaller right">
  ![](/images/2014-07-18-menu.png)
  <figcaption>You can find "Settings" in the cog menu.</figcaption>
</figure>

Travis CI puts a cap on how many builds can run for your project at the same time. Previously, this solely depends on the number of builds running for the same account. The maximum number on [travis-ci.com](https://travis-ci.com) depends on your plan, on [travis-ci.org](https://travis-ci.org) it depends on the overall system load.

We have now added the option to limit the number of concurrent builds on a per project bases. Just head over to the recently launched [Settings pane](/2014-03-05-repository-settings/), and you will find a new input field there.

This feature will of course not allow you to go beyond the account limit, but you will be able to reduce the number of builds for your project.

<figure>
  ![](/images/2014-07-18-settings.png)
  <figcaption>The [Settings pane](/2014-03-05-repository-settings/) now allows you to limit the number of concurrently builds per project.</figcaption>
</figure>

There are a few reasons why this can be a good idea:

* You can avoid builds running in parallel by setting the concurrency to 1. This might be useful if your build is depending on an external resource and might run into a race condition with concurrent builds.
* A single repository will not use up all your account's builds. This might be useful when working in larger organizations.

As always, this feature is also available [via our command line client](https://github.com/travis-ci/travis.rb#settings):

    $ travis settings maximum_number_of_builds --set 1

We are continuously working on a better CI experience, so let us know what you think!