---
title: Slack Build Notifications
layout: post
permalink: 2014-03-13-slack-notifications
author: Mathias Meyer
twitter: roidrage
created_at: Thu 13 Mar 2014 18:00:00 CET
---
[Slack](http://slack.com) just recently launched to the general public with
their team chat system. It has a neat user interface and some unique features as
well, but it's also very hacker-friendly by way of its integration for external
services, the API, and the IRC/XMPP bridge.

They even launched with support for Travis CI out of the box, thank you, Slack!

But the previous integration required using webhook URLs rather than utilizing
our common format for notifications.

Today we're more than happy to change that, as Slack are now a built-in part of
[our notification system](http://docs.travis-ci.com/user/notifications).

Getting started requires a new [Slack integration for Travis
CI](https://my.slack.com/services/new/travis).

Once you've chosen a room, you'll get a snippet ready to copy and paste into your
`.travis.yml`.

![](http://s3itch.paperplanes.de/Team_Integration__Travis_CI_Slack_20140313_093329_20140313_093404.jpg)

You can set up multiple notifications to multiple channels too.

We did something new with this integration as well: **Slack notifications are
sent on pull requests**, so your team can stay up-to-date about their build
status.

Check our
[documentation](http://docs.travis-ci.com/user/notifications/#Slack-notifications)
for the full details on how to configure Slack notifications.

Happy shipping!
