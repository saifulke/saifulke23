---
title: How to Get Over the Fear of Shipping
layout: post
author: Mathias Meyer
twitter: roidrage
created_at: Fri 31 Jan 2014 15:30:00 CET
permalink: 2014-01-31-how-to-over-the-fear-of-shipping
---
<figure class="right normal">
  <img src="http://farm8.staticflickr.com/7174/6432758331_e5fef60899_n.jpg">
</figure>

In a [previous post, we asked whether you're afraid of
shipping](/2014-01-17-are-you-afraid-of-shipping/). We sincerely hope you
aren't.

But if you find yourself having **doubts when deploying changes to production**
or want to **increase your confidence** overall, read on!

The fear of shipping, as I like to call it, is a Medusa with lots of heads. So
many things can creep into your code, your tests, your process or your
production environment, that can reduce you and your team's confidence to ship.

Let's look at some of the most common impediments to shipping code with
confidence.

### Lack of tests

Unfortunately good test coverage is not a given yet in this day and age.

Maybe you've taken over a legacy code base, maybe you had to rush out a feature
but didn't add tests. Test coverage can decay for a lot of reasons, but seeing
it go down over time will decrease your confidence in shipping.

Tests may never fully be able to reproduce the behaviour your code will show in
production. But they allow you to prove to yourself and your team that the
general workings of your code and any changes.

If your project lacks tests, start right now. **Get into the habit of writing
tests for any new code you're writing and for any existing code you're
changing.**

There are excellent services out there to [track your code
coverage](https://codeclimate.com/partners/travisci).

If you're looking into adopting a continuous integration system, [we can help
with that too](https://travis-ci.com)!

### Lack of automated deployment

How fast can you ship your code to production? Does it take minutes?

How often do you deploy? Once a month? Once a week? Once a day?

The Code Climate team cut down [their deployment time to 5
seconds](http://blog.codeclimate.com/blog/2013/10/02/high-speed-rails-deploys-with-git/).

Is your deployment automated? How long does it take? What can you speed up?

The faster you can deploy new code, the more confident your team will be in
making and shipping changes.

**Fast deployments ensure that code can be deployed quickly, but that it can be
fixed quickly too.**

### Lack of monitoring

The strangest things happen to the best-intentioned code as soon as it's exposed
to the harsh world that is production.

When you deploy changes to production, are they ready for monitoring? Can you be
confident that the code is doing what it's supposed to do?

Monitoring, just like writing tests, tends to fall off the Kanban boards quickly
as soon as a deadline looms.

But without any monitoring in place, how can you be confident that your code
doesn't crash in production, that it takes down the database by way of a new
query introduced by a recent change?

**Good monitoring is hard, but without it, you'll be flying blind.**

### Long-lived feature branches and large changesets

How long does it take new features or changes to move to production? Are your
pull requests long-lived? Are changes usually made in big commits rather than in
small, incremental steps? Do you tend to squash a long series of commits into
one or a few more big commits?

Long-lived feature branches can be a burden to shipping. The longer they live
the harder it is going to be to see their effects on your application in
production. The longer they're around the longer it's going to take for your
company to see the value of a change to its customers.

Long-lived feature branches squashed into a small series of commits can pose
similar challenges. But what's worse is they make it a lot harder to debug
changes introduced in them. Smaller commits shipped to production allow it to
rollback quickly and to inspect the code changed rather than going through a
long history of code to figure out where things went wrong.

How long does it take for any change in your code base to get to production? How
long to feature branches exist? How often do your developers commit directly to
master? Can you push new features to production, being able to test them in
isolation, without direct customer impact?

**Keeping changes small, adding feature flags for them can help you ship changes
to production faster**. You can work on new features incrementally and try them
out without directly impacting your customers initially.

### Complex dependencies

Over the last two years, we split up Travis CI into lots of smaller apps. While
this was great help to scale out the platform, there was an effect we initially
didn't foresee.

Most of the apps depend on one large library containing all code, it's called
travis-core.

Whenever something in that repository changes, we ideally need to deploy all our
apps to production to make sure the change doesn't impact any of them.

This **big, single dependency is an impediment to us shipping code, and it's a
common problem**.

Do your projects have a common dependency, a library of shared code?

We're slowly breaking this part up, pulling the relevant code into all of our
single apps rather than share a big bundle amongst all of them. While this may
cause some duplication, it allows us to ship faster in return and with more
confidence.

The duplication is outweighed by every app only knowing about our data model
what it needs to. We can reduce database models to the information relevant to
each app, slowly replacing direct database access with API access, an
architecture where every app knows as little as possible about the others and
about the overall data model.

### Slow test suites

Slow tests can be a true burden. A test suite that takes more than ten minutes
to run will slow down your ability to ship. The longer developers have to wait
to see the effect of their changes on the code base, the longer it'll take for
them to ship changes to production.

Slow test suites can be a great opportunity to get a coffee, but they can be
very disruptive to the flow of making changes, of building new features, of
adding more customer value.

**Slow tests are a productivity killer**.

If you look at your test suite, what could you take away and still ship code to
production with confidence? What could you change to speed them up?

### Shipping isn't everything, but being able to is important

When your team can ship changes to production quickly and with confidence,
you'll not only make them more productive, you'll make them happier. With
happier developers, focused on customer value, you'll have happier customers.

Everybody wins.
