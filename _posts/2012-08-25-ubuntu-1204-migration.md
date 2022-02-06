---
title: Upcoming CI Environment Updates
layout: post
created_at: Sat Aug 25 12:00:00 CDT 2012
permalink: /august-2012-upcoming-ci-environment-updates
author: Michael Klishin
twitter: michaelklishin
---

An important part of Travis CI is our [CI environment](http://docs.travis-ci.com/user/ci-environment/): all the runtimes, tools, libraries and system configuration that
projects rely on to run their test suites. While considered to be the most mature part of Travis CI (we are at v5.1 at the moment),
it still moves fast. Today we want to give you a heads-up on important recent and upcoming changes:

 * CI username change
 * Disabling some services (e.g. MongoDB, Riak, RabbitMQ) on boot
 * Migration to Ubuntu 12.04
 * Migration to 64 bit VMs


## CI Username Change

On August 25th, we deployed new VM images that change CI username from `vagrant` to `travis`. If your project depends on

 * The exact system username
 * or `$HOME` pointing to `/home/vagrant`

then you need to update your `.travis.yml` and/or build scripts to use the environment variables `USER` and `HOME` instead. Depending on exact values of those variables
is usually not necessary: the best way to detect that you are running in the Travis CI environment is by checking if either (or both) `CI` and `TRAVIS` env varibales
are set. If you feel adventurous, feel free to use [`HAS_JOSH_K_SEAL_OF_APPROVAL`](https://github.com/travis-ci/travis-cookbooks/blob/master/ci_environment/travis_build_environment/files/default/ci_user/travis_environment.sh#L8-9) instead ([Josh K is a real person](https://twitter.com/j2h)).


## Disabling Most Services on Boot

Currently when we boot the VMs we use, a number of services are started:

 * MySQL
 * PostgreSQL
 * RabbitMQ
 * MongoDB
 * Redis
 * Riak
 * CouchDB

and so on. Each might individually consume a small amount of resources, but in total they consume a non-trivial amount of RAM. This limits both 
the amount of RAM available to your test suites and our ability to move some parts of the environment (for example, MySQL and PostgreSQL data directories) 
to RAM-based file system mounts to speed up test suites that are very heavy on I/O and in particular random access I/O (think Ruby on Rails or Django). 
Tuning configuration of services to consume less RAM is possible but it is very hard to pick good defaults for all 
of them.

In addition, most projects and test suites don't use these services. Because of this we will be turning off most services
on boot, leaving only MySQL and PostgreSQL running. Note that we already do this for some services 
(for example, Cassandra, Neo4J, ElasticSearch).

If your project needs, say, MongoDB running, you can the following to your `.travis.yml`:

    services: mongodb

or if you need several services, you can use the following:

    services:
      - riak     # will start riak
      - rabbitmq # will start rabbitmq-server
      - memcache # will start memcached

This allows us to provide nice aliases for each service and normalize any differences between names, like RabbitMQ for example. Note that this feature only
works for services we provision in our [CI environment](http://docs.travis-ci.com/user/ci-environment/). If you download, say, Apache Jackrabbit and
start it manually in a `before_install` step, you will still have to do it the same way.

The change will go into effect on the 14th of September, 2012 and we encourage all Travis CI users to make changes to their `.travis.yml` as soon as possible as to avoid any issues, as well as being forward-compatible.


## Distribution Versions: A Brief History Lesson

When we first started using virtual machines for Travis CI (around June 2011) we decided to use Ubuntu 10.04. 
This worked perfectly, but by the fall of 2011 10.04 started showing its age. Our users kept asking for more 
recent versions of certain tools and libraries which were challenging to provide without building and maintaining 
a myriad of Debian packages. So in November 2011 we migrated all VMs to Ubuntu 11.04 which solved the problem. 
And then in early April 2012 we [migrated to 11.10](/upcoming_ubuntu_11_10_migration/).

Now it is August 2012 and the time to move on to 12.04 is drawing close. We want to explain briefly how Travis CI 
will migrate to it, why we are doing it and what may change for your project.


## Why Migrate?

With Ubuntu 12.04, we will be able to provide more up-to-date versions of tools and services in our CI environment, 
including:

 * MySQL 5.5
 * CouchDB 1.2
 * Updated Git

and many others. In addition, we hope to be able to provision Python 3.3 preview releases (there are 12.04 packages 
we can use).


## Staying One Step Behind, Intentionally

Our users are mostly software developers and they tend to like staying up-to-date with tools, services, libraries and 
so on. However, production environments are rarely on the bleeding edge. So for CI in general, and Travis CI in 
particular, it is important to maintain a balance: not too old, but not too new either. This is why Travis CI is 
intentionally several months behind Ubuntu releases. It gives developers several months to catch up with recent 
changes, fix issues and push out new releases.


## Notable Changes in 12.04

12.04 is a significantly smaller change that 11.10 has been: no breaking changes to fundamental libraries like 
OpenSSL, no [major or minor] GCC version changes, et cetera.

### MySQL Server

12.04 provides MySQL Server 5.5. Most projects should keep working without any changes.


### System Perl

System Perl version changes to 5.14. This won't matter for Perl projects on Travis CI (we use a separate set 
of Perls provisioned with [Perlbrew](http://perlbrew.pl/)) but projects in other languages that use Perl as 
part of their build system may be affected.


### System Erlang/OTP

System Erlang/OTP version changes to R14B04. This won't matter for Erlang projects on Travis CI (we use a 
separate set of OTP builds provisioned with [kerl](https://github.com/spawngrid/kerl)) but projects in other 
languages that may rely on Erlang as part of their build system may be affected.


### Bison 2.5

Projects that use Bison may need to check for 2.5 compatibility.


## The Road To 12.04

Travis CI environment will transition to 12.04 in the first week of September, 2012.


## Migrating CI Environment to 64 bit

The current Travis CI environment is 32 bit. This works fine for most cases but has a few downsides:

 * The majority of developers and projects target 64 bit first because this is their deployment environment of choice.
 * Some runtimes are primarily used in 64 bit environments and their 32 bit counterparts have stability issues that are outside of our control.

Because we already work towards freeing more RAM for project test suites to use, we decided it is a good time to also move to 64 bit.
The exact migration date is not yet decided, but most likely this will happen in late September or early October 2012.


## Getting Help

If you have questions, please ask them on our [mailing list](https://groups.google.com/forum/?fromgroups#!forum/travis-ci) or in
`#travis` on chat.freenode.net.


Happy testing!


The Travis CI Team
