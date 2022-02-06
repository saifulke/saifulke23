---
title: "Manage Private Dependencies More Easily"
created_at: Mon 25 Aug 2014 16:00:00 CET
author: Piotr Sarnacki
twitter: drogus
layout: post
permalink: 2014-08-25-manage-private-dependencies-more-easily
---

When testing a private repository, you may need to fetch private dependencies,
like a private git submodule. A common approach to authorize a submodule is to use a private key
with access to multiple repositories on GitHub.

Until recently, the only way to set a custom SSH key was to put it in the `.travis.yml` file.
However, there were security concerns attached to this approach.

In order to improve that we're introducing a way to add an SSH key in the UI:

<figure>
  [ ![SSH Key screen in the Repository Settings](/images/ssh-key-screen.png) ](/images/ssh-key-screen.png)
  <figcaption>SSH Key screen in the Repository Settings</figcaption>
</figure>

After clicking "Add a custom SSH key" you can add a key which will be then used in
your builds:

<figure>
  [ ![Adding an SSH Key in the Repository Settings](/images/ssh-key-screen-add.png) ](/images/ssh-key-screen-add.png)
  <figcaption>Adding an SSH Key in the Repository Settings</figcaption>
</figure>

To make it easier to identify the SSH key in use we also display a fingerprint in the build logs now:

<figure>
  [ ![SSH Key fingerprint in logs](/images/ssh-key-fingerprint.png) ](/images/ssh-key-fingerprint.png)
  <figcaption>SSH Key fingerprint in logs</figcaption>
</figure>

## Security

The SSH key added through the UI is securely stored in our DB in an encrypted form.
To reduce any possible attack vector, we recommend using a user with as little
access as possible to only the repositories used as dependencies.

## Other ways to add private dependencies


We hope that you will find the new UI addition useful. If there's anything
else you would like to know about this specific way of dealing with dependencies
or find out what are the alternatives, we created a documentation page on the subject:
[Private dependencies](http://docs.travis-ci.com/user/private-dependencies/).
