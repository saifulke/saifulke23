---
title: "New Deployment Providers"
author: Joshua Anderson
created_at: Fri 17 May 2014 00:00:00 PST
layout: post
permalink: /2014-05-16-new-deployment-providers
---

The Travis CI team has been busy adding several new providers for continuous deployment: [Modulus](https://modulus.io/), [GitHub Releases](https://github.com/blog/1547-release-your-software), [Ninefold](https://ninefold.com/), [Cloud 66](https://www.cloud66.com/) and a major rewrite for [Cloud Foundry](http://cloudfoundry.org/index.html).

When we launched continuous deployment with Heroku 10 months ago, we had no idea how fast it would grow. Now, we're up to 19 providers, with more landing every few weeks.

### Modulus

To get started deploying to Modulus add the following to your `.travis.yml`.

    deploy:
      provider: modulus
      api-key: <Modulus API Key>
      project-name: <Modulus Project Name>

 We recomend you encrypt your [encrypt your `api-key` in your `.travis.yml`](http://docs.travis-ci.com/user/encryption-keys/).

You can always use the `travis` tool to set this up as well.

    $ travis setup modulus

To read more about deployment to Modulus you can go [here](http://docs.travis-ci.com/user/deployment/modulus).

### GitHub Releases

When you create a git tag, Travis CI can automatically upload your files to the resulting GitHub Release. Here is a minimal `.travis.yml` to get you started.

    deploy:
      provider: releases
      api-key: <GitHub Oauth Token>
      file: <File to Upload>
      skip_cleanup: true
      on:
        tags: true
        all_branches: true

We especially recommend using the `travis` tool to set up GitHub Releases, as it will automatially setup a oauth key with the correct scopes and encrypts it for you.

    $ travis setup releases

To read more about deployment to GitHub Releases you can go [here](http://docs.travis-ci.com/user/deployment/releases).

### Ninefold

It's easy to get started with Ninefold. Just add the following to your `.travis.yml`.

    deploy:
      provider: ninefold
      auth-token: <Ninefold Auth Token>
      app-id: <Ninefold App ID>

 We recomend you encrypt your [encrypt your `auth-token` in your `.travis.yml`](http://docs.travis-ci.com/user/encryption-keys/).

As always, you can use the `travis` tool to set everthing up for you.

    $ travis setup ninefold

To read more about deployment to Ninefold you can go [here](http://docs.travis-ci.com/user/deployment/ninefold).

### Cloud 66

Cloud 66 is super easy to setup. Just find your redeployment hook url in the information menu within the Cloud 66 portal. Then, add that url to you `.travis.yml` as shown.

    deploy:
      provider: cloud66
      redeployment_hook: <Redeployment Hook URL>

 We recomend you encrypt your [encrypt your `redeployment-hook` in your `.travis.yml`](http://docs.travis-ci.com/user/encryption-keys/).

To read more about deployment to Cloud 66 you can go [here](http://docs.travis-ci.com/user/deployment/cloud66).

### Cloud Foundry Update

A ton of work took place behind the scenes with the Cloud Foundry provider. We switched from the deprecated ruby library to thier new go library. If you're using cloud foundry currently, you'll need to rename the `target` variable to `api`.

To read more about deployment to Cloud Foundry you can go [here](http://docs.travis-ci.com/user/deployment/cloudfoundry).


### Keep Up the Great Work!

This release never could have happened without our awesome community. Send a **huge** round of applause to Mariana Lenetis, Zachary Gershman, Matt Hernandez, Nicholas Bruning, Nigel Ramsay, and Joshua Anderson.

### Is your provider still missing?

We've been adding support for lots of new providers, but there are still plenty more out there.
If you'd like to support for your cloud provider on Travis CI, please [shoot us an email](mailto:support@travis-ci.org).

Or, send us a pull request over at our [dpl repository](http://github.com/travis-ci/dpl).