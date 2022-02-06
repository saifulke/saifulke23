---
title: "Minor language updates - September 2014"
created_at: Wed 3 Sep 2014 20:41:09 EDT
author: Hiro Asari
twitter: hiro_asari
layout: post
permalink: 2014-09-03-minor-language-update
---

Three minor language updates are scheduled at 
**[14:00 UTC on the 5th of September](http://everytimezone.com/#2014-9-5,120,cn3)**
for both [travis-ci.org](https://travis-ci.org) and [travis-ci.com](https://travis-ci.com).

## Perl VM

1. `ExtUtils::MakeMaker` is updated to the latest version in all runtimes (6.98 as of this writing).
1. The `5.18-shrplib` and `5.20-shrplib` runtimes now has the extra `-Duseithreads` compile-time flags,
and they are also known as `5.18-extras` and `5.20-extras`.

## PHP VM

5.6.0 was [officially released](http://php.net/archive/2014.php#id2014-08-28-1) on 28th of August,
and we will offer this version pre-installed with this update.

`xdebug` will be updated to 2.2.5 on PHP 5.3.3 and 5.5.9 to be the same as the other php environments.

We've also updated phpunit to 4.2.4 on the php/hhvm machines to fix some regreations in phpunit 4.2.2.
