---
title: How Finer-Grained Metrics in a High Traffic Component Helped us Uncover a Code Bug
permalink: 2014-08-26-how-finer-grained-metrics-in-high-traffic-component-helped-uncover-bug
author: Mathias Meyer
twitter: roidrage
created_at: Tue 26 Aug 2014 11:30:00 CEST
layout: post
---
A few weeks ago, we had spurious alerts go off at fairly regular intervals,
usually even at the same time of day, when our open source platform was busiest.

One of our production alerts looks at the queue size of log message chunks
waiting. Those can pile up quickly when something goes wrong, delaying live log
updates when they do.

This started happening out of the blue, so we were very suspicious.
Unfortunately our metrics didn't show us much, as they're aggregated from all
dynos processing the chunks. As a quick fix we increased the number of processes
plowing through them, which reduced the number of occurrances but didn't make
the pain go away.

Looking at our RabbitMQ console, we noticed that some processes had less open
channels than others, meaning that they get closed for some unknown reason,
reducing the number of concurrent messages each process can handle, eventually
causing messages to queue up.

### How did we find the problem?

We pulled a trick from a previous blog post we pushed a few weeks ago, on [how
you can aggregate metrics across multiple Heroku
processes](http://blog.travis-ci.com/2014-07-08-three-ways-to-aggregate-metrics-on-heroku/).

We started tracking more fine-grained metrics for every dyno, based on the dyno
number that's stored in the `$DYNO` environment variable. We soon noticed in the
metrics when certain processes suddenly dropped in their message processing
volume. In the graph below, you can see that before the first set of annotations
(an annotation is added every time one of our apps is deployed), there was only
a single metric tracking the aggregated processing volume.

![](http://s3itch.paperplanes.de/BsACCKLCYAAmiEC-large.jpeg_2014-08-25_13-45-55_2014-08-25_13-49-39.jpg)

With the first two annotations we deployed the change to get more metrics
detail. Normally the processing should be fairly smooth, but this graph shows
erradic behaviour of a few dynos. Normally, all processes should process a
somewhat equal amount of messages, as RabbitMQ distributes messages on a
round-robin basis for all open channels.

Now we were able to correlate these drops with the logs, and soon we found errors
of when channels were closed. We found a fix quickly and haven't had any alerts
since.

You can see where the fix was deployed around the second set of annotations on
July 4th. 

Having these more detailed metrics helped us figure out a problem much better
and faster than our accumulated metrics did. **For dynos with a high processing
volume, make sure to have enough detail in your metrics to find culprits on
level as low as possible.**

**Alert fatigue is a real problem**, any increase in alerts should be warning
sign for your team to investigate the issue as soon as possible. With
**increasing spurious alerts, attention is drawn from the important production
issues.**

### What was the culprit?

So what caused the issue in the end?

A bug was introduced (by me!) in the message handling. When an error occured
parsing a message, and we noticed these errors in the logs around the time the
message processing dropped, some messages were acknowledge twice, which caused
an error from RabbitMQ and closed the channel, lowering the number of threads
processing messages every time.

The fix turned out to be just [moving the acknowledge of the message outside of
a retry
block](https://github.com/travis-ci/travis-logs/commit/a5b67d6bf7201ae9490b1324951af04ae05cade7)
we were using to catch errors related to writing to the database. Simple, yet
very much facepalm-worthy.

It all boiled down to the finer grained metrics in these high volume processes
to eventually find and fix the culprit.
