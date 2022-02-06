---
title: Why is my build not running? Introducing greater transparency in why we accept or reject builds
layout: post
author: Piotr Sarnacki
twitter: drogus
permalink: /2014-05-12-why-is-my-build-not-running
created_at: Mon 12 May 2014 15:00:00 CEST
---

Sometimes you push to Travis CI and there is no new build. What to do in such case?
Has Travis CI got your commits? Is the branch you were using disabled? Do you need
to tweak some settings? You no longer need to ask these questions!

We prepared a better way to see what's happening on Travis CI after you push to Github.
The new requests page shows all of the events which we got for a given repository, be it
pushes or pull requests:

![Requests page for travis-web project](http://drogus-s3itch.s3.amazonaws.com/requests-page-20140512-131215.png)

There is also a possibility to view requests using CLI `travis requests` command:

![Requests on CLI](http://drogus-s3itch.s3.amazonaws.com/1._Shell-20140512-135610.png)

In order to view requests page on Travis CI web client you can use "cog menu" on the upper right:

![Cog menu requests item](http://drogus-s3itch.s3.amazonaws.com/Travis_CI_-_Free_Hosted_Continuous_Integration_Platform_for_the_Open_Source_Community-20140512-135953.png)

If you are not sure if your commits reached Travis CI don't wait and checkout the requests page!
