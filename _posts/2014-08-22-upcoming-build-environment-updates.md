---
title: "Upcoming Build Environment Updates -- August"
created_at: Fri 22 Aug 2014 11:47:30 EDT
author: Hiro Asari
twitter: hiro_asari
layout: post
permalink: 2014-08-22-upcoming-build-environment-updates
---

We have added a lot of nice changes to our cookbooks recently, so
we decided to roll out the updates to you sooner rather than later!

Here are details of the August, 2014 updates.

## Update

Due to JDK bug discussed below, Oracle JDK 7 will remain at 7u60,
and Oracle JDK 8 at 8u5.

Even though OpenJDK 7u65 contains the bytecode verifier bug,
we are unable to offer a reasonable alternative without it.
Setting environment variables `_JAVA_OPTIONS=-Xverify:none` or
`_JAVA_OPTIONS=-XX:-UseSplitVerifier` should mitigate this issue.

## Update

This announcement originally mentioned MongoDB update from 2.4.x to 2.6.4.
We discovered a problem with the plan, however, and decided to postpone
this MongoDB update until we can provide a more solid upgrade plan.
We apologize for the inconvenience, and thank you for your understanding.

## Update schedule

The updates will be rolled out to
**[travis-ci.org](https://travis-ci.org)** at **[14:00 UTC on the 27th of August](http://everytimezone.com/#2014-8-27,120,cn3)** and
to **[travis-ci.com](https://travis-ci.com)** at **[14:00 UTC on the 29th of August](http://everytimezone.com/#2014-8-29,120,cn3)**.

## Build Environment Updates

All environments will receive the following updates:

### Chromium browser

34.0.1847.116 → 36.0.1985.125

### CouchDB

1.5.0 → 1.6.0

### ElasticSearch

1.1.1 → 1.3.2

This change contains breaking changes: [1.1 → 1.2](http://www.elasticsearch.org/blog/elasticsearch-1-2-0-released/),
[1.2 → 1.3](http://www.elasticsearch.org/downloads/1-3-0/).

If you need to revert to ElasticSearch 1.1.1 because of these breaking changes,
remove the installed version and install 1.1.1:

```yaml
before_install:
  - sudo apt-get purge elasticsearch
  - curl -O https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.1.1.deb
  - sudo dpkg -i elasticsearch-1.1.1.deb
```
### Firefox browser

Included is an update to the latest Extended Support Release (ESR),
31.0esr, which corresponds to Desktop Firefox 31.0.

### MySQL

5.5.37 → 5.5.38

### OpenJDK 6

6b31 → 6b32

### OpenJDK 7

7u55 → 7u65

### PostgreSQL

1. 9.1.13 → 9.1.14
1. 9.2.8 → 9.2.9
1. 9.3.4 → 9.3.5

### RabbitMQ

3.3.4 → 3.3.5

### Sphinx

1. 2.2.2-beta → 2.2.3-beta
1. 2.1.8 → 2.1.9

## Android VM

Android SDK is updated to 23.0.2.
`build-tools-20.0.0` is pre-installed.

### Gradle 2.0

Gradle has been updated to version 2.0.
This release contains potential breaking changes.
If you need to go back to version 1.11, add the following to your `.travis.yml`:

```yaml
before_install:
  - sudo rm -r /usr/local/gradle
  - curl -LO http://services.gradle.org/distributions/gradle-1.11-bin.zip
  - unzip -q gradle-1.11-bin.zip
  - sudo mv gradle-1.11 /usr/local/gradle
```

## Haskell VM

Platform is updated to 2014.2.0.0.
GHC 7.8.2 is updated to 7.8.3. (Other versions remain the same.)

## Java VM (not JVM)

* Maven is updated to 3.2.3.
* Leiningen2 is updated to 2.4.3, which is now the default.

### Gradle 2.0

See notes [above](#gradle-20).

### Leiningen will default to 2.x

With this update, the default version of Leiningen will be 2.4.3.
Leiningen 1.x will be available as `lein1`.

`lein` will point to Leiningen 2.4.3, but `lein2` will also be available as before.

Those repositories which use `lein` need to be updated to invoke `lein1` instead.

### Scala

Scala is updated to 2.11.2, sbt to 0.13.5.

In addision, Scala 2.9.2 and 2.10.2 are preinstalled.
These versions address problem with cross-compilation, and build failures
descriebed in http://www.typesafe.com/blog/what-happened-to-my-travis-ci, respectively.

## PHP VM

Version updates include:

* 5.6.0rc4
* 5.5.16
* 5.4.32
* 5.3.29

We've also added 5.5.9 back. This is the version supported on Ubuntu LTS14.04.

## Go forth and test!

Happy testing!

Love,

Travis Team
