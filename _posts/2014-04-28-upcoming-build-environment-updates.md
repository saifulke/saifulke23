---
title: Upcoming Build Environment Updates
author: Josh Kalderimis
twitter: j2h
created_at: Mon 28 Apr 2014 14:00:00 CEST
layout: post
permalink: /2014-04-28-upcoming-build-environment-updates
---

**Update: The build environment update for travis-ci.com has been postponed by two days (7th of May, 02:00 UTC) due to some fixes required in the Ruby build environment.**

We are very excited to announce a great set of updates to our Build Environment for all Travis CI users.

These updates include everything from version bumps in the services we provide, to language build environment improvements.

## Update schedule
These build environment updates will be live for all **[travis-ci.org](https://travis-ci.org)** users at **04:00 UTC on the 30th of April**, with **[travis-ci.com](https://travis-ci.com)** due to be updated on the **7th of May at 02:00 UTC**.

## Update highlights

There are two updates we would like to talk about in further detail.

### HHVM nightly builds

The first is the inclusion of HHVM nightly in the PHP build environment. This means you can now add:

    php:
      - hhvm-nightly

to your .travis.yml and we will install the latest nightly HHVM package so you can test your libraries or apps against the latest and greatest changes available in trunk. On top of this we have also updated the installed HHVM to 3.0.1.

[Loic Frering](https://twitter.com/loicfrering) has been instrumental in adding this feature to Travis CI, as well as his amazing work in keeping the PHP build environment up to date with the latest PHP versions.

### Python updates

Our second piece of exciting news is the Python build environment has had a major upgrade thanks to [Donald Stufft](https://github.com/travis-ci/travis-cookbooks/pull/284) from Rackspace.

Our Python setup previously used packages supplied by [deadsnakes](https://launchpad.net/~fkrull/+archive/deadsnakes), as well as the system Python packages for Python 2.7 and Python 3.2.

Under the hood we have changed to using [python-build](https://github.com/yyuu/pyenv/tree/master/plugins/python-build) which opens up the options for installing multiple patch versions of each minor version of Python.

With this update you now have access to Python 2.6.9, 2.7.6, 3.2.5, 3.3.5 and 3.4.0, as well as PyPy 2.2.1.

## A special thanks!

Lastly we would love to give huge thanks to [Gilles Cornu](https://github.com/gildegoma) who has been a tremendous help in upgrading our cookbooks and our language build environments. Gilles, you rock!

If you're having any problems after the upgrade, please [file an issue](https://github.com/travis-ci/travis-ci/issues/new) or [contact
support](mailto:support@travis-ci.com) directly.

Have a fantastic week,

Josh


### Summerized Build Environment Updates

Below is the full set of changes included in this upgrade:

**Erlang**:

  - Removed 17.0-rc1 and 17.0-rc2
  - 17.0 added

**Python**:

  - Pythons now installed with pyenv
  - 3.4.0 is now available
  - 2.6.9, 2.7.6, 3.2.5, 3.3.5, 3.4.0, pypy-2.2.1 all installed

**PHP**:

  - Updated PHP to 5.4.27 and 5.5.11
  - Support for PHP 5.6 with 5.6.0alpha3
  - Updated HHVM to 3.0.1
  - Support for HHVM nightly

**Ruby**:

  - JRuby upgraded to 1.7.11
  - 1.9.3 upgraded to 1.9.3-p545
  - 2.0.0 upgraded to 2.0.0-p451
  - 2.1.0 upgraded to 2.1.1

**Perl**:

  - Updated 5.19.6 to 5.19.9
  - Updated 5.18.1 to 5.18.2

**Haskell**:

  - 7.8.2 added

**Java**:

  - Updated Oracle JDK 8 to build 1.8.0-b132
  - JCE for JDK 8 added
  - Updated Maven to 3.2.1

**Scala**:

  - Updated sbt launcher
  - 2.10.4 now the default and preinstalled

**Node.js**:

  - Updated nvm
  - 0.10.26 is the new default
  - Updated 0.11 to 0.11.11

**C/C++**:

  - Clang updated to 3.4

**Services**: (standard on all language build environments)

  - Elasticsearch 1.1.0
  - CouchDB 1.3.1
  - MongoDB 2.4.10
  - Redis 2.8.8
  - Riak 1.4.8
  - RabbitMQ 3.3.0-1
  - Memcached 1.4.13
  - Cassandra 2.0.5
  - Neo4j 1.9.4
  - Kestrel 2.3.2
