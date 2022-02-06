---
title: Send Your Build Notifications to Sqwiggle
created_at: Wed Feb 12 2014 18:00:00 CEST
author: Mathias Meyer
twitter: roidrage
permalink: 2014-02-12-send-your-build-notifications-to-sqwiggle
layout: post
---
Just recently, in a blog post on [how we manage remote
work](/2014-02-03-how-we-manage-work-in-a-remote-team/), we introduced you to
[Sqwiggle](https://www.sqwiggle.com), a great tool for remote teams to stay in
visual touch with each other./

Sqwiggle supports more than video presence and video chats, you can use it as
your team's event and message feed as well.

Last week the Sqwiggle team [announced their new
API](https://www.sqwiggle.com/news/announcing-the-sqwiggle-api), which you can
now use to push events into your team's streams from an external source.

Today we're happy to ship support for pushing Travis CI build results into your
Sqwiggle streams!

First up, make sure you've [signed up for a Sqwiggle
account](https://www.sqwiggle.com/#signup). It's free to try and free for teams
of up to three people. Next, create an [API
client](https://www.sqwiggle.com/company/clients).

Make sure to copy the API token shown as it will only be shown to you once.

Then you can enable the notifications in your `.travis.yml`:

    notifications:
      sqwiggle: <api_token>@room

The room can be identified by its path name or by its identifier, which you can
fetch via the API.

The path name is easier to fetch, you just need to copy the last part from the
URL of the room you're in.

Here's the resulting stream with a few build notifications trickling in.

![](http://s3itch.paperplanes.de/sqwiggle_20140212_101419.jpg)

Be sure to [encrypt these
credentials](http://docs.travis-ci.com/user/encryption-keys/) using our
[travis](https://github.com/travis-ci/travis) command line tool.

You can notify multiple Sqwiggle rooms too, just add the `rooms` key and specify
the list of rooms.

    notifications:
      sqwiggle:
        rooms:
          - <api_token>@situation-room
          - <api_token>@main-hall

Our thanks to [Luke](https://twitter.com/lukeroberts1990) from Sqwiggle for contributing the notifications code!
