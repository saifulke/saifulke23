---
title: "Environment Variables"
created_at: Fri 22 Aug 2014 10:00:00 CET
author: Konstantin Haase
twitter: konstantinhaase
layout: post
permalink: 2014-08-22-environment-variables
---

A common way to customize the build process is to use environment variables. These can be accessed from any stage in your build process.

<figure>
  [ ![Environment Variables in the Repository Settings](/images/settings-env-vars.png) ](/images/settings-env-vars.png)
  <figcaption>Environment Variables in the Repository Settings]</figcaption>
</figure>

Up until now, variables could only be set in the **.travis.yml**. We are happy to announce that as of today, you can also set environment variables via the [repository settings pane](/2014-03-05-repository-settings/).

## Two kinds of variables

Variables in the **.travis.yml** are bound to a certain commit. Changing them requires a new commit, restarting an old build will use the old values. They will also be available automatically on forks of the repository.

On the other hand, variables defined in the **repository settings** are the same for all builds. When you restart an old build, it will use the latest values. These variables are not automatically available to forks.

Keep this in mind when choosing where to store which variable.

Examples for using the **.travis.yml**:

* Variables generally needed for the build to run, that don't contain sensitive data. For instance, a test suite for a Ruby application might require `$RACK_ENV` to be set to `test`.
* Variables that have to differ per branch.
* Variables that have to differ per job.

Examples for using **repository settings**:

* Variables that have to differ per repository.
* Variables that contain sensitive data, such as third-party credentials.

## Priority

If a variable set with the UI has the same name as a variable set in the .travis.yml, the latter will have priority. That way you can overwrite whatever is set in the UI, for example if you need to use a different value in a branch.

## Displaying the value

By default, the value of these new environment variables will be hidden from the `export` line in the logs. This corresponds to the behavior of encrypted variables in your .travis.yml.

Similarly, we do not expose these values to untrusted builds, triggered by pull requests from another repository.

## The settings pane

As you might have noticed, we are adding more and more functionality to the settings pane. There is a strategy behind this.

Our plan is not to abandon the .travis.yml, or give you a second interface to it. We believe that having your build instructions under version control, side by side with your code, is a simple and powerful principle.

But there are settings which are not part of the build itself, which might be related to the repository itself rather than the code at a certain stage. This is the guiding principle we have been using lately to decide whether a feature should go into the .travis.yml or the settings pane. And this is also why we came to the conclusion that it's best to have two places for defining variables.
