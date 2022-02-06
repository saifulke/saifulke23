---
title: Using Feature Flags to Ship Changes with Confidence
layout: post
author: Mathias Meyer
twitter: roidrage
permalink: /2014-03-04-use-feature-flags-to-ship-changes-with-confidence
created_at: Tue 4 Mar 2014 18:00:00 CEST
---
Continuous integration is all about the entire team committing to master daily.

Small changes, shipped to production quickly, rather than living on feature branches, increase the velocity of new features and bug fixes reaching your customers.

But with most changes merged directly to master, how can you build new features with the confidence that shipping them won't have any impact on your customers, and only make it available once you're confident it's ready for prime time?

In a feature branch world, your new feature would be in the works for a while, changes are continuously merged in from master, making sure not to break anything.

But you won't know until it's finally merged and deployed to production whether your changes work.

**How can you continuously ship new features to production with the confidence of not impacting your customers?**

The answer is: **feature flags**.

A feature flag is a branching point that your code can utilize to determine whether or not a feature should be made available to one or more customers.

The original approach was made popular by the [fine folks at Flickr](http://code.flickr.net/2009/12/02/flipping-out/). They needed a means to disable features when something is broken in production, to reduce the load on the database or on other parts of the system.

But feature flags can be used for much more than just disabling features in production.

* Enable a feature only for a specific number of users, or even just for yourself to try it out in isolation.

* Trial a new feature for a sample set of customers to compare how they're using it compared to the previous version of the feature.

    This allows you to run experiments with actual users before you put it live. You can collect feedback and iterate based on real production usage.
   
* Enable it for your team to try out and give feedback on. At GitHub, this is known as staff mode. Next time you see a hubber in the wild, peek at their version of GitHub, I'm sure you'll notice some subtle differences.

* Enable a feature for a specific set of users, or just your team for them to try it out before it's rolled out for everyone.

When a feature finally is rolled out for everyone, you can decide case by case on whether you want to leave a global feature flag so you can disable a new feature in the future.

The three use cases can even be put together. First you roll out a new feature for yourself, so you can try it out in production. Next you enable it for your team, and then you enable if for a subset of users. Finally, you make it available for everyone.

### How do I implement feature flags?

At the core, feature flags are simple configuration settings with Boolean values.

    if Travis::Application.config.features.repository_settings?
      # code to handle settings
    end

This example uses a Rails built-in means to manage application configuration, storing flags as simple true/false key value pairs.

For a Rails project, you can store this configuration in an initializer file.

    # config/initializers/features.rb
    Travis::Application.config.features = {
      repository_settings: true
    }

For every new feature, you can add the setting here, leaving all of them in one place to find, disable and enable them easily. All it takes is one change and a redeploy to enable or disable a feature.

This mechanism allows you to only fully disable or enable something, and only with redeploying the entire app, which can sometimes be burdensome. It also lacks the finesse to enable features for specific users or groups of users.

### Flagging features at runtime

A more dynamic approach is to store the feature configuration in either an ephemeral or permanent storage, like Redis or your database, respectively.

Assuming your code continuously checks feature flags at runtime, all it takes is changing a value in the central configuration service and it can have an immediate affect on the running application without requiring a restart.

[James Golick's rollout](https://github.com/FetLife/rollout) is a popular library to implement dynamic feature flags for Ruby applications. It allows you to enable features for specific users, groups of users, a percentage of users, or disable and enable them entirely. Hey, that library covers all of our bases!

Not coincidentally, it's the one we're using for Travis CI.

Rather than store the data in a configuration file, you can store them in Redis, or any supported key value store. Instead of asking the application's configuration, you ask rollout whether a feature is enabled.

    if rollout.active?(:repository_settings, current_user)
      # settings logic goes here
    end

Enabling a feature for a user is just as simple.

  rollout.activate_user(:repository_settings, User.find_by_login('roidrage'))

You can segment users into groups as well, based on the flags a specific users. Our friends at [Librato](https://librato.com) use a mechanism similar to this for segmenting out users they'd like to test new features before they're available for everyone, the beta list if you will.

    rollout.define_group(:beta_testers) do |user|
      user.beta?
    end

### Document feature flags

When feature flags are collected using a centralized store like Redis, it gets harder to track which flags are available, what their defaults should be, and which features they affect.

Make sure to keep simple documentation around where you collect feature flags to make sure the right ones are changed at the right time.

### Feature flags at Travis CI

We're using rollout for our feature flags, but we've added a few more things that we need. Some features on Travis CI are only made available for certain repositories or certain accounts and all of their respective repositories.

Most of our feature flags are built for production runtime though. We have means to enable build scheduling, for instance during a maintenance, without taking down the entire process. That way we can still process actively running builds without scheduling new ones.

We've used feature flips to migrate to different implementations of something too. Originally, our user synchronization went through RabbitMQ and was handled by the same process that handles scheduling builds.

As we switched over to a process based on Sidekiq, we enabled our own users first to make sure the process works, before we finally enabled it for everyone. We eventually moved the feature flip, as the code that originally handled this part was deleted as well.

We're also using them to enable [custom subscription plans](https://travis-ci.com/plans) for some of our customers.

### Ship with confidence

**Feature flags are very handy to roll out new features gradually, but they also give you higher control over your system running in production as well.**

New features, even in raw shape, can be put to use and test in the production environment as soon as something is ready for trying out, and without impacting users unless you choose to.

On top of that, they give you a means to disable certain features during a production incident.

Is your project using feature flags or a similar means? Feel free to share your experiences in the comments.
