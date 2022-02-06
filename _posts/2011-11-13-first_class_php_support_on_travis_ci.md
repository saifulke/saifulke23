---
title: Announcing "first class" PHP project support!
layout: post
created_at: Sun Nov 13 12:08:00 EDT 2011
permalink: /first_class_php_support_on_travis_ci
---

Today we are happy to announce first class PHP support with Travis CI.

It includes all the same features Ruby, Erlang and Node.js projects enjoy today, including:

 * Easy to get started and integrates with GitHub.
 * Test against multiple databases and services, including MySQL, Postgres, Redis, RabbitMQ and many more.
 * Test your projects against multiple PHP versions.
 * Build results are publicly available online so you can link to them in your bug reports, including line numbers.
 * Notifications the way you want them! (email, IRC, and webhooks)

Over the last several weeks many nice folks from the PHP community have been working with the Travis team
and it would not be possible without all the help from [Loïc Frering](https://twitter.com/loicfrering) and [Pascal Borreli](https://github.com/pborreli). [Till Klampaeckel](https://github.com/till) has helped us set up [phpfarm](http://sourceforge.net/p/phpfarm/wiki/Home/) and [pyrus](http://pear2.php.net/) and test drive the whole thing. [Álvaro Videla](https://twitter.com/old_sound) and
[Lukas Kahwe Smith](https://github.com/lsmith77) also helped us a lot by running some of the [Friends of Symfony](https://github.com/friendsofsymfony) projects on Travis early on.
Pascal also got Symfony, Twig, Silex, Doctrine and Monolog test suites up and running on travis-ci.org (we hope his patches will be accepted
upstream).

Having all those projects building fine for several days makes us confident that we are ready to ship this feature.

Please see our [initial documentation for PHP projects](http://docs.travis-ci.com/user/languages/php) and [the rest of the guides](http://docs.travis-ci.com/). We tried to link to as many real world .travis.yml examples to demonstrate all the features in action.

In addition, we have a couple of machines lined up that we will be running PHP builds on. One of them is [Shopify](http://shopify.com): they donated a worker we have been using for Node.js projects. Another one is [ServerGrove](http://servergrove.com), experts in PHP hosting and specifically frameworks like Symfony and Zend Framework: they donated us one more machine to run PHP builds on.

If you have questions, find us in #travis on chat.freenode.net, we will be happy to answer them. To stay up to date with new announcements, CI environment software updates and more, [follow us on Twitter](https://twitter.com/travisci) and [join our mailing list](https://groups.google.com/forum/#!forum/travis-ci).

We hope you enjoy using Travis for your open source projects as much as we do. Go add your PHP projects to Travis CI and recommend your fellow PHP developers to do the same!

The Travis Team.


## Spread the word!

Feel free to [discuss and upvote on Hacker News](http://news.ycombinator.com/item?id=3231030)


## Updates

 * Doctrine is now on Travis: [doctrine2](http://travis-ci.org/#!/doctrine/doctrine2), [common](http://travis-ci.org/#!/doctrine/common)
 * Monolog is now on Travis [Monolog](http://travis-ci.org/#!/Seldaek/monolog)
