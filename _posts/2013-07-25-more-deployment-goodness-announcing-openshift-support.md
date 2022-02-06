---
title: "More Deployment Goodness: Announcing OpenShift Support!"
author: Aaron Hill
created_at: Thu 25 Jul 2013 20:15 CET
layout: post
permalink: /2013-07-25-more-deployment-goodness-announcing-openshift-support
---

Remember a little while back when we introduced support for [deploying to Heroku](/2013-07-09-introducing-continuous-deployment-to-heroku) and [Nodejitsu](/blog/2013-07-22-deploy-your-apps-to-nodejitsu)?

We thought "why stop there"!

We are excited to announce that you can now deploy to [OpenShift](http://openshift.com) from your Travis builds!

To set up continuous deployment to Openshift, add the following lines to your `.travis.yml`:

    deploy:
      provider: openshift
      user: "YOUR-EMAIL-ADDRESS"
      password: "YOUR-PASSWORD" # encrypted, of course
      app: "YOUR-APP-NAME" # optional if it's the same as your repo name
      domain: "YOUR-OPENSHIFT-DOMAIN"

Or, if your have [our command line tool](https://github.com/travis-ci/travis) installed, use the new `setup` command:

    $ travis setup openshift

That's it!

To provide the best service possible, Travis CI has teamed up with OpenShift as a [partner](https://www.openshift.com/partners) and there is an official [Travis CI QuickStart](https://www.openshift.com/quickstarts/travis-ci-on-openshift) to get you going.

This feature is immediately available to all our users including our [Travis Pro](http://travis-ci.com) customers.

For more information, see [the documentation](http://docs.travis-ci.com/user/deployment/openshift).

### Your provider still missing?

If your cloud provider isn't supported by Travis CI, please [let us know](mailto:support@travis-ci.org).

Or, if you're so inclined, add support yourself and [send us a pull request](https://github.com/travis-ci/dpl).
