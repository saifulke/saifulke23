---
title: Travis CI Gets a Little Rusty
permalink: 2014-09-3-travis-ci-gets-a-little-rusty
author: Josh Kalderimis
twitter: j2h
created_at: Wed 3 Sep 2014 4:30:00 CEST
layout: post
---

We are very pleased to announce official Rust language support when you
test your project on Travis CI.

<figure class="smaller right">
  ![Travis CI Mascot: The Rust Edition](/images/2014-09-3-travis-gets-rusty.png)
  <figcaption>Travis CI Mascot: The Rust Edition</figcaption>
</figure>

This is available for both open source and private repositories right now.

For a while now we have seen the rise of developers
[testing Rust projects](http://bettong.net/2014/05/09/how-to-test-rust-on-travis-ci/)
on Travis CI, usually by installing Rust and Cargo as required, and then running
`cargo build` and `cargo test`.

With the awesome help of [dyrim](https://github.com/dyrim), who was very kind
to send us a [Pull Request](https://github.com/travis-ci/travis-build/pull/264)
to wrap these defaults, including the installation of Rust and Cargo, all you
need to do is add:

    language: rust

to your `.travis.yml` file and you are good to go!

By default this will test your project by installing Rust and Cargo nightly
binaries. If you need a specific version, all you need to do is add the
following to your `.travis.yml`:

    language: rust

    rust: 0.11.0

and BOOM!, you are now testing against version 0.11.0 of Rust.

But what if you want to test against 0.11.0 and nightly?

    language: rust

    rust:
      - 0.11.0
      - nightly

We can hear you right now screaming 'How delightful!', but that's not all!

As always you get all the awesome power of Travis CI, including the ability to
override the install and script steps.

For example, if you don't want Travis CI to run `cargo build` and `cargo test`,
all you need to do is change your `.travis.yml` file to:

    language: rust

    script: ./run_my_favourite_script

We have added [full documentation](http://docs.travis-ci.com/user/languages/rust/)
on our Rust support in case you have any further questions.

Have a fantastic Tuesday,

The Travis CI Team
