---
title: The Three Ingredients of a Great Postmortem
layout: post
created_at: Thu 26 Jun 2014 15:00:00 CEST
author: Mathias Meyer
twitter: roidrage
permalink: 2014-06-26-three-ingredients-to-a-great-postmortem
---
Writing a postmortem is the biggest courtesy you can do to your users. If
something has impacted their ability to use your product, they should know why
and what you're doing to reduce the impact of similar circumstances in the
future.

A good postmortem includes three parts, and they're best structured based on the
three R's: **regret, reason, and remedy**. I was introduced to the three R's by
reading ["Drop The Pink Elephant"](http://amzn.to/1p6RBpi), a book that
encourages clarity in communication with others, in this case, your customers.

Let's look at every R in more detail.

### Regret

It should go without saying that your empathy levels with your customers went
through the roof as things went down. The stress levels surely rose quickly, as
everyone's focused on restoring what's broken.

Saying that you're sorry is the number one courtesy, no matter what the problem
is. That much the book ["How To Win Friends and Influence
People"](http://amzn.to/SXYMWu) has taught me.

As humans, we still find it surprisingly hard to tell someone we're sorry. While
it doesn't undo damage, it helps to rebuild trust, as you're acknowledging that
something on your side caused grief or even just the customers' inability to use
your product.

Start out with apologizing and acknowledging that the outage has caused your
customers trouble, as it very likely has.

### Reason

This is your moment of glory.

This should be the outline of what happened. How granular you go depends on the
audience and on how willing your organization is to share.

The more detail you add, the more value your postmortem has to your customers as
they'll be assured you know what the issues were leading up to the outage. The
amount of detail depends on your customers, a customer base made of developer or
ops folks may appreciate detail more than consumers.

But you're also doing the rest of the operational community a service, as others
get to learn from your experiences.

Towards your customers, openness and honesty is a courtesy. There's no point in
hiding details because it's embarrassing.

Postmortems help your organization accept that it has problems to solve. The
reasoning helps not just your customers, it helps your organization as well.

##### Things that don't belong here:

Don't throw anyone under the bus, neither one of your team members nor a vendor.
What happened is on you, and on you alone. While blaming someone else might feel
like a relief, it's your site, it's your availability, it's your organization's
problem to take care of it.

Blaming anyone individual or a vendor doesn't help, it just distracts from the
issue at hand, and it doesn't help your customers either.

#### Side Note: There is no root cause

When postmortems try to find a root cause, they're fooling themselves into
thinking that there's only one problem, and that this problem can be fixed.

Most, if not all, production outages have lots of contributing factors that come
into play. Decisions that were made months or years ago can eventually help
trigger an issue that no one could foresee at the time.

When you add other factors that may or may not be in your control, those
decisions can eventually contribute to a production outage.

**[There is no root cause, there are lots of little things that come together to
cause
grief.](http://www.kitchensoap.com/2012/02/10/each-necessary-but-only-jointly-sufficient/)**

### Remedy

Ideally you've developed a plan of attack on the issues the outage has
uncovered, whether they're at the organizational or at the technical level.

Saying "you're working to prevent this won't happen again" is insufficient, as
you can neither guarantee that nor does it include any specific goal.

The purpose of the remedy is to tell your customers that your team is working on
improving the situation, that you have a sense of what needs to be done to
reduce the impact of future outages.

Again, technical details are a nuance that depends on your customer audience. 

Sometimes, you may even end up in a position where you're not certain what the
remedies should be, as you haven't yet fully understood the impact of the
problem. It's okay to admit that, but you should commit yourself to continue the
investigation and add more monitoring, logging, metrics, to help you understand
the issue should it happen again.

**The three R's, regret, reason, and remedy, are the key ingredients to a good
postmortem**. They give a good general structure and a guide of what you should
tell your customers after an outage.

Looking for some great postmortems for inspiration?
[Here](https://github.com/blog/1796-denial-of-service-attacks),
[I've](https://status.heroku.com/incidents/642)
[got](http://blog.dnsimple.com/2014/02/incident-report-ams-feb-2014/)
[you](https://aws.amazon.com/message/67457/)
[covered](http://boundary.com/blog/2012/08/01/riak-kobayashi-post-mortem/).

Want to learn more about how to write awesome postmortems? Dave Zwieback is
giving a [workshop in NYC on July 10th
2014](https://ti.to/mindweather/awesome-postmortems) on this very topic. His
paper on ["The Human Side of
Postmortems"](http://www.oreilly.com/webops-perf/free/the-human-side-of-postmortems.csp)
is required reading.
