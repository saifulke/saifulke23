---
title: "Improved Artifacts; Like Dinosaurs, But Cooler"
author: Dan Buch
created_at: Tues 09 September 2014 00:00:00 GMT
layout: post
permalink: /2014-09-09-improved-artifacts-like-dinosaurs-but-cooler
---

*Dan has been a long-time contributor to Travis CI, including not only our Go
support, but also features within our cookbooks, as well as how we originally
supported uploading artifacts after a build.  We're very honored to have him
not only help us ship this feature, but also write this blog post, which I'm
sure you'll all enjoy.  ~ [Josh Kalderimis](https://twitter.com/j2h)*

If the builds you're running on Travis CI produces artifacts, you'll no doubt
be thrilled to hear that we want to make saving these artifacts super easy for
you.

The first supported tool for doing this was
[travis-artifacts](https://github.com/travis-ci/travis-artifacts), a handy
gem-installable tool for shipping artifacts to Amazon S3.  This was a great
start, and solved the immediate need, but we knew we could do better.

Among the problems we hoped to address were the lengthy installation process of
runtime dependencies and the lack of first-class support in one's
`.travis.yml`.

What we ended up building comes in two parts.  First, there is a binary
executable called `artifacts`.  This binary may be downloaded and used directly
by following the [installation
instructions](https://github.com/travis-ci/artifacts#installation).

In addition to this binary, an `artifacts` addon was tacked onto
[travis-build](https://github.com/travis-ci/travis-build) so that you can use
it via your `.travis.yml`.  More details are available in [the
docs](http://docs.travis-ci.com/user/uploading-artifacts/), for example, all
you need is to add the following to your `.travis.yml`:

``` yaml
addons:
  artifacts:
    bucket: my-special-bucket
    key:
      secure: SyaIXy6OKDaYiew+...5vgAldy3jkmKA=
    secret:
      secure: X19eaiiFZobD3uCk...X8cY+ohT8WkQ0=
```

And you should then see at the bottom of your log:

![Artifacts upload in
action](/images/2014-09-09-artifacts-upload-travis-log.png)

*The above screenshot is from
[travis-build](https://travis-ci.org/travis-ci/travis-build/builds/32925401).*

You can also set `ARTIFACTS_KEY` and `ARTIFACTS_SECRET` environment variables
via the repository settings in order to keep your `.travis.yml` more slim, for
example:

![Artifacts env vars in repository
settings](/images/2014-09-09-artifacts-env-vars.png)

Setting such environment variables would reduce the valid addons configuration
to the following:

``` yaml
addons:
  artifacts:
    bucket: my-special-bucket
```

By default, any files found using `git ls-files -o` within your repository
directory will be uploaded to S3.  If you want to upload a different set of
files, you can specify these using the following config:

``` yaml
addons:
  artifacts:
    # ...
    paths:
    # arbitrary shell commands are supported, but the output should be
    # converted to a ':'-delimited string.
    - $(ls /var/log/*.log | tr "\n" ":")
    # singular paths work fine, too
    - $HOME/some/other/path.log
```

We have some great improvements in the works to make artifacts even better, but
consider this the first of many.

We're looking forward to hearing what you think!
