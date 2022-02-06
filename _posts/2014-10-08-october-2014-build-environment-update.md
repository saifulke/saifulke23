---
title: "October 2014 Build Environment Update"
created_at: Wed 08 Oct 2014 08:40:38 EDT
author: Hiro Asari
twitter: hiro_asari
layout: post
permalink: 2014-10-08-october-2014-build-environment-update
---

# Scheduled Updates

We plan a new wave of build environment updates.

The updates will be rolled out to
**[travis-ci.org](https://travis-ci.org)** at **[14:00 UTC on the 9th of October](http://everytimezone.com/#2014-10-9,120,cn3)** and
to **[travis-ci.com](https://travis-ci.com)** at **[14:00 UTC on the 14th of October](http://everytimezone.com/#2014-10-14,120,cn3)**.

*****
### Update
PHP images will be updated with the following updates:

* HHVM has been updated to 3.3.0.
* PHP 5.5.17 and 5.4.33 are now installed.

This will be rolled out to .org at the same time .com update is scheduled.
*****

The updates will include the following:

## All build environments except PHP environments

* bash has been updated to include the [CVE-2014-7169](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-7169) fix.
* Go has been updated to 1.3.3.
* Sphinx 2.2.4 is available.

Please note that we have postponed updates to PHP environments due to older sources
(in particular, 5.2.17 and 5.3.3) currently being unavailable on [PHP archive](http://museum.php.net).

## Erlang VM

* Erlang 17.3 is added.

## Java VM

* Leiningen is updated to 2.5.0.

## Node.js VM

* Version 0.10.32 is pre-installed and now the default.

## Ruby VM

* JRuby is updated to 1.7.16.

## Questions or comments?

As usual, please get in touch if you have questions or comments.

Happy testing!

Love,

Travis CI Team
