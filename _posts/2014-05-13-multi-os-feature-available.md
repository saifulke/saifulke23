---
title: "Multi-OS Feature Available"
created_at: Tue 13 May 2014 06:30:09 EDT
author: Hiro Asari
twitter: hiro_asari
layout: post
permalink: 2014-05-13-multi-os-feature-available
---

## Update: We are not currently accepting multi-OS requests
We are at capacity with Mac workers in both .org and .com
environments.
Consequently, we are not accepting requests for the multi-OS
feature at this time.
As more capacity is added, we will resume accepting requests.

### Update

This blog post originally promised that Python libraries can be tested
on OS X workers.
That was incorrect.
We apologize for this inaccuracy.

## One Repository, Multiple Operating Systems
We are elated to announce the availabity of the multi-OS feature
on Travis CI.

With this feature, your code can now be tested on Linux and Mac OS
workers.
Your Ruby gems, C programs, and Java libraries
can now be tested on Travis CI from a single repository.

## "Cool beans! How do I get started?"
The mulit-OS feature is currently in beta testing, and
must be manually turned on by the Travis CI team on a
repository-by-repository basis.

If you want the feature turned on for your repository, get in
touch with us via email at [support@travis-ci.com](mailto:support@travis-ci.com).

### What Sort of Repositories are Best Suited for this Feature?

Repositories most suitable for this feature are those with small build
matrices, and without requirement for multiple language run times.

## Modify Your `.travis.yml`
Once you have your repository has the multi-OS feature on, all you
have to do is add these lines to your `.travis.yml`:

```yaml
os:
  - linux
  - osx
```

This will double the size of your [build matrix](http://docs.travis-ci.com/user/build-configuration/#The-Build-Matrix)
and start running your code on both Linux and Mac OS X workers.

## Caveat Emptor
When you test your code on multiple OSes, always be mindful of differences
that can affect your tests.

1. Not all tools may be available on the Mac

	We are still working on building up the tool chain on the Mac worker.
	Presently, Ruby is the most supported language across the OSes.

1. The file system behavior is different

	The HFS+ file system on our OS X workers is case-insensitive (which is the factory default),
	and the files in a directory are returned sorted.
	On Linux, on the other hand, the file system is case-sensitive, and returns directory entries in
	the order they appear in the directory internally, which may appear random.

	Your tests may implicitly rely on these behaviors, and could fail because of them.

1. They are different operating systems, after all

	Commands may have the same name on the Mac and Linux, but they may have different flags,
	or the same flag may mean different things.
	In some cases, commands that do the same thing could have different names.
	These need to be investigated case by case.

## Huge Thanks to Facebook

This feature was supported by [Facebook](https://code.facebook.com/).
Thank you, Facebook, for your support of Travis CI!

## Problems?
As always, if you run into problems or have suggestions, open a [GitHub issue](https://github.com/travis-ci/travis-ci/issues/new).

Happy Testing!
