---
title: Six Ways to Make Your Production Logs More Useful
created_at: Fri 11 Apr 2014 11:30:00 CEST
layout: post
author: Mathias Meyer
twitter: roidrage
permalink: 2014-04-11-fun-with-logs/
---
Logs are the soul of any application running in production. They give you a means to trace what's been happening in a particular request or a user's activity throughout your system.

They're incredibly handy. Just figure out what to log, print it to a log of your choice. You even get a timestamp for free.

To make finding things even easier, aggregating your logs allows you to trace something across multiple apps on multiple hosts.

But logs can be a bit more than just boring one liners telling you fun stories of `this shouldn't happen`, `--- MARK ---`, or the cheerful `last message repeated 5 times`. They can be turned into a useful source of data. Heck, logs can even be fun.

### Log structured data in a readable format

Don't get me wrong, I do enjoy reading prose in logs. Finding a good narrative and following it can be a pleasant surprise, especially compared to the good old `about to finish` or that print debugging statement someone forgot in the code.

However, for certain things, using a more structured logging format can come in handy.

Instantly, JSON comes to mind, but seriously, is JSON really a readable format? For machines, certainly, but for humans? It's a terrible format to read.

For a long time, I've enjoyed reading the output from [Heroku's](https://www.heroku.com) router. A simple key=value format (the = is real!) that lets you log kind of structured data in a format that's pretty easy to parse for the human eye and for a machine too.

Heroku also coined the idea that [logs are more than just files, they're streams](https://adam.heroku.com/past/2011/4/1/logs_are_streams_not_files/).

The router's log format was an inspiration to build [lograge](https://github.com/roidrage/lograge), a little library that scraps Rails' default logging format, which is terrible to make sense of in production, and replaces it with simple one-liner logs.

Logging structured data with this format only requires a hash of key=value pairs and to output them to whatever log facility you're using.

Here's an example from the Heroku router:

    heroku[router]: at=info method=POST path=/ host=billing.travis-ci.com
      dyno=web.1 connect=3ms service=148ms status=303 bytes=614

Here's the request as logged with lograge:

    method=GET path=/ format=html controller=home action=index status=200
      duration=200.95 view=164.48 db=30.98

Add a unique request identifier to the mix and you can start tracing requests throughout your system, both with a log parser, which can make sense of the format above, and with your eyes when you're tailing or searching the logs.

### Add a dash of color

Logs can be fun too, and fun requires a dash of color, no doubt.

While this may not be for the faint of heart, or log purists, should they exist, this can add a nice salience to your logs, allowing the eye to differentiate better between different levels and types of data.

Our own build logs support a lot of ANSI codes too, allowing you to see your build output in all its colorful goodness. Everybody likes a green build, right?

All it takes is adding a few ANSI escapes to your logs. Here's an example from our support backend:

    \e[32m[admin] \e[33m[#{request_id}] \e[35m[#{current_user.login}]\e[0m

Every ANSI escape starts with a `\e` escape sequence followed by a command, in this case `[32m` which tells the terminal to change the graphics mode. At the end, `\e[0m` resets the graphics mode back to the default.

The example above outputs an identification string for the application, then the request's identifier and the current user's login name. The first string is assigned the color green, the next orange-yellow and the last in magenta.

The result looks like this when viewed in [Papertrail](https://papertrailapp.com):

![](http://s3itch.paperplanes.de/ansilogs_20140411_105032.jpg)
  
The downside of adding too much color to your logs is that your eyes might get distracted by the color, and information might get lost. Don't overdo it, but color can be useful in small dashes.

Adding to that, when looking at a plain text log with a terminal or viewer that doesn't render ANSI escapes, they'll clutter your log, which can be unpleasant.

[ANSI controls](http://ascii-table.com/ansi-escape-sequences.php) can be quite useful, even beyond your logs. You can even make your build tools or your test runs more fun. Think [Nyan Cat for your RSpec build output](http://www.mattsears.com/articles/2011/11/16/nyan-cat-rspec-formatter).

### Logs let your app communicate with you and your team

As you're a normal human being, you probably won't be staring at your logs all day. It can be fun at times, certainly, but let's face it, you'll have better things to do.

Being aware of some things your application is logging without resorting to a search can be quite handy, and maybe your logs could even let you know when something is up?

Enter aggregated search systems like [Papertrail](https://papertrailapp.com), [GrayLog2](http://graylog2.org), and the like.

They allow you to set filters for certain log patterns and notify you when they come up.

This is quite handy both for alerting, but also to keep your team in the loop on things like new customers.

At [Travis CI](https://travis-ci.com), our billing system logs a specific line whenever a new customer signs up for a paid plan or when a customer upgrades their plan.

This, accompanied by a Campfire sound, makes for a delight every time it happens, for everyone who's currently in the Campfire room.

### Seriously though, don't put exception stack traces in your logs!

If you've ever worked in a Java environment, you've probably looked at pages and pages of stack traces in log files. Heck, you've probably seen those in Ruby apps, or any language that creates stack traces with exceptions.

**Logs are no place for exception stack traces.**

Why? Most logs, at least in the traditional sense, are file based or are at least streamed line by line, as they are on Heroku. That means that most logging statements are focused on some sort of single action that fits into a line, more or less.

Exception stack traces, on the other hand, to be in any way readable, need lots of newlines. The fun starts when long exception backtraces are intermingled with other log lines, making it almost impossible to piece them back together. Sure, you can prefix every line with a unique identifier, but that still means you have to collect that information and search for that identifier just to get a stack trace.

That's so tedious, and it's why exception stack traces shouldn't end up in logs in the first place.

Instead, log the fact that an error occurred. The exception itself should be sent to a tracking service like [Sentry](http://getsentry.com), [Honeybadger](http://honeybadger.io), or any of the others out there. Hint: we're using Sentry.

For an added bonus, log a unique identifier that's associated with the exception itself and that's also transmitted to the exception tracking service. Now you have additional context to piece logs and exceptions together. Even better, and only when you have all the information, log a direct URL that can be accessed to get to the exception.

### Log URLs for easy access to more context

Speaking of URLs, logging them can be incredibly handy. Of course not just any URL, but the ones that make it easier to access any information that could help investigate a problem further.

Our billing system logs links to customer information on Stripe, for example. Taking this further, your application could log links to your support backend, where the person currently investigating the case could learn more about the customer who's affected.

### Add emotional context to your logs

Emojis are great to [express your emotions](http://wynnnetherland.com/journal/putting-the-emote-in-remote-work) and to say things much shorter than with words.

That should give us something for logs as well, shouldn't it? It's nice to parse web request log lines that show something like `status=500`, but how much better would it be if they said `status=`:scream:?

Or replace severity with emojis. Surely :cry: is easier to spot for your eyes than `WARN`, yes?

Of course you could easily use [Kaomojis](http://www.chatslang.com/emoticons/kaomoji) as well, should your favorite logging system or terminal not support Emojis. `status=(╯°□°）╯` or `status=ಠ_ಠ` could work just as well.

Logs are incredibly useful, and you can even have some fun with them too. Be nice to your logs and always **keep in mind the person who's reading them when something requires investigation or even in stressful outage situations**. Making logs useful requires a lot of work but it pays off much later down the line, when something needs to be investigated.
