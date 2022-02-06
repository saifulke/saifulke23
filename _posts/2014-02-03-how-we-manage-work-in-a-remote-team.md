---
title: How We Manage Work in a Remote Team
twitter_card_image: "http://s3itch.paperplanes.de/Sqwiggle_20140117_192032.jpg_20140203_152335.jpg"
author: Mathias Meyer
twitter: roidrage
created_at: Mon 3 Feb 2014 16:00:00 CET
permalink: 2014-02-03-how-we-manage-work-in-a-remote-team
layout: post
---
The roots of Travis CI are in open source. In that part of the world,
communicating via chat, email and tickets is quite natural.

When we started grouping as a company two years ago, using these means for
communication came quite natural. One of us was in Amsterdam (or in New Zealand,
depending on the time of day), the others in Berlin.

Still, setting up a Campfire for us to chat in was one of our first steps.

As our team grew, we faced some challenges though. What came natural for us at
first turned into a core value of our company, and we have to work hard on
keeping it like that.

Today we have a few people in Berlin/Germany, sometimes working from home, other
times working from our little office, one person in Poland, one in North
Carolina, one part time in Vienna, another one in Ohio, and that guy in New
Zealand, too.

I want to share some of the challenges we faces continuing to make this work,
both in terms of our tooling and interaction between humans.

### The virtual water cooler

Most of our team communication evolves around Campfire. We have one common room,
the water cooler, if you will, and some separate rooms. One to talk about
design-related issues, another one for live support with our customers (The
Lounge), another one to handle outages and production incidents (The Panic
Room), and a room to discuss operational and administrative issues (The
Situation Room).

Most importantly, we have a little [Hubot](http://hubot.github.com) sitting
there, ready to take commands.  We use it for a lot of things, to [update our
status
page](http://blog.travis-ci.com/2013-07-08-operating-your-site-with-hubot/)
during a production incident, to interact with our alerting system, to remind us
of certain tasks, even just remind ourselves to remind others of certain tasks.

But what it also does is help raise team spirit. You'll be surprised what a
simple pug bomb or even just a Google image search for "fresh pots" can do to
get everyone a good laugh.

Campfire is our virtual water cooler. Everyone hangs out there most of the time,
but people can choose to leave to get work done. It is a distraction, and it's
up to everyone to take a leave when they feel like they need to get work done.

There's an abundance of tools to enable teams to communicate remotely,
[HipChat](http://hipchat.com), [Slack](http://slack.com),
[Grove](http://grove.io), and good old IRC, to name a few.

### Communication is asynchronous

Whether you're chatting via Campfire, discussing a pull request, or sending
emails on certain things, communication is always asynchronous.

This is quite hard to get used to, and I speak from personal experience.

Talking about features, discussing issues gets a bit more casual. For whatever
reason they might have, people won't always be able to immediately respond to a
question, to a problem or an animated GIF.

A big part of our workflow is going through GitHub issues. Both because our open
source is our nature, and because we chose it as the simplest tool that could
possibly work.

Anything is discussed in GitHub issues. New features, sponsorships, new hires,
administrative things, blog posts, outages. There's an issue for anything. It's
much easier to keep a public and searchable paper trail, accessible by everyone
on the team, than to keep all this in personal email boxes.

But responses to issues won't always be immediate. They also have the added
downside of adding quite a lot of noise to an email inbox.

Remember: **a pull request or even an issue thread is best served with an
animated GIF.**

### Face time is invaluable

Even working remotely, communicating with people face to face beats all other
means of communication.

When something needs to be discussed, smaller teams form and discuss things in a
small circle.

We have one weekly team call, where everyone gets together for some face time,
though time zones don't always permit everyone being on the same call.

We currently use Google Hangouts for these purposes, but it's unfortunately a
terrible experience. Friends have recommended alternatives to us, among them
[Zoom](http://zoom.us), [Blue Jeans](http://bluejeans.com),
[Dozeo](http://dozeo.com) and [FuzeBox](https://www.fuzebox.com/). We'll try out
some of the alternatives and will report back on our findings. Putting 10
different video streams together is no easy feat, but facetime is essential.

At last year's FutureStack conference, GitHub's Streaming Eagles gave an
[inspiring talk on supporting remoting
workers](http://www.youtube.com/watch?v=cU49ToHyFcU) by bringing them closer to
each other. A must watch, if you ask me.

I found one thing in particular very interesting. They talked about a video
presence system they have in place. Its purpose is to give a live feed of
everyone who's working remotely. They don't have to talk, they don't have to
look at the feed all the time.

But the feed gives your team something quite powerful, it brings your remote
workers closer together. The solitude of the home office is converted into a
place where you can see your co-workers, talk to them anytime, but there's no
obligation to do anything.

Just **seeing faces can have a big impact on team happiness.**

We've been trialing [Sqwiggle](http://www.sqwiggle.com) recently, a product that
gives you both a feed of everyone on your team, with pictures updating every
couple of seconds, and the ability to start a video chat with up to four of your
team mates at any time.

<figure class="right normal">
  <img src="http://s3itch.paperplanes.de/Sqwiggle_20140117_192032.jpg_20140203_152335.jpg"/>
</figure>

Here's a feed of the Travis CI team, hard at work. Which is to say, looking at
animated cat GIFs.

While we're on the topic of animated GIFs. They may be silly to some, but they
can be an incredibly effective tool to raise team spirit at once. I'm guilty of
bombing our Campfire room with GIfs occasionally, and their means of bogging
down any CPU with rendering can be an annoyance, but they can give everyone a
good laugh.

Same for emojis (which [Wynn from GitHub recently wrote
about](http://wynnnetherland.com/journal/putting-the-emote-in-remote-work)), pug
bombs and a simple `/awwww` command in Campfire.

### Remote work is about happiness

<figure>
  <img src="http://s3itch.paperplanes.de/sliceoflife.gif"/>
</figure>

With a remote team, you need to invest a lot more to make your team happy, to
give them room to bond when they don't see each other in person for weeks or
months, to give them a good laugh every now and then.

Tools like [Hubot](http://hubot.github.com), [Campfire](http://campfirenow.com),
[Sqwiggle](https://www.sqwiggle.com), and [GitHub](http://github.com) play an
important part in our remote life. We're constantly working on improving our
tool set to make it easier for our team to work together.

What are your favorites?
