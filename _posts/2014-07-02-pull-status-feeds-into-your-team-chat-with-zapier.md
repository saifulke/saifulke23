---
title: Pull Status Feeds Into Your Team Chat with Zapier
created_at: Wed 2 Jul 2014 16:00:00 CEST
author: Mathias Meyer
twitter: roidrage
layout: post
permalink: 2014-07-02-pull-status-feeds-with-zapier
---
When your business relies on infrastructure hosted and run by other companies,
keeping an eye on their operational status. Most of them have a status page, but
it's almost impossible to keep an eye on all of them.

These days, most teams use some form of team chat though, whether it's
[Slack](https://slack.com),
[Campfire](https://campfirenow.com) or [HipChat](https://hipchat.com). These serve as more than a team communication platform,
they allow interacting with a bot and pull in data from external services like
GitHub (or Travis CI!).

So why not use them as a means to pull in status feeds? Most status pages offer
some sort of RSS feed, so let's use that.

We started setting up Zaps on [Zapier](https://zapier.com) for this purpose.
Their service can pull in RSS feeds and digest new articles, spitting them into
another service, like the most common team chat services. Here's a Zap to [pipe
new items from an RSS feed to
HipChat](https://zapier.com/zapbook/rss/hipchat/627/hipchat-alert-from-rss-feed/),
or the [same one for
Slack](https://zapier.com/zapbook/rss/slack/33119/rss-new-item-in-feed-to-slack-send-new-message/).

Here's how to set up an alert for the [Heroku status
feed](http://status.heroku.com).

First, select the "New item in feed" action for RSS and the "New message" for
your chat system of choice.

![](http://s3itch.paperplanes.de/Editor_-_Zapier_2014-06-28_18-01-17_2014-06-28_18-01-43.jpg)

Follow the next steps, select a chat system account, and enter
`https://status.heroku.com/feed` as the feed's URL.

![](http://s3itch.paperplanes.de/Editor_-_Zapier_2014-06-28_18-03-34_2014-06-28_18-03-37.jpg)

When it comes to assembling the message that's output into your team chat, you
can keep it simple. Just the title and the link is keeping it short and
succinct, giving direct access to more details.

![](http://s3itch.paperplanes.de/Editor_-_Zapier_2014-07-02_16-15-37_2014-07-02_16-15-45.jpg)

Follow the remaining steps, and voila, your team will always be up-to-date on
the status of the infrastructure providers your application relies on.
