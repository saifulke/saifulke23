---
title: "Introducing Finer Controls over Building Branches and Pull Requests with Repository Settings"
created_at: Wed 05 Mar 2014 18:30:00 CET
author: Piotr Sarnacki
twitter: drogus
layout: post
permalink: 2014-03-05-repository-settings
---

A `.travis.yml` config file is a main configuration point for your builds.
It's a really powerful tool with lots of options and possibilities and it
has been doing its' job tremendously. There are some settings, however,
which doesn't fit there as well as others.

Sometimes it's much easier to set a setting for a repository globally, for
all of the branches. Some settings, like notifications, can also make it hard
to work between forks. There is also a case of vulnerable data, such as API keys
or passwords, which you can store securely in a `.travis.yml` file only after
encrypting it.

We're aware of those shortcomings and we would like to start tackling them with
repository settings kept on Travis CI servers which can be configured
through the API, our web client or Travis CLI.

We started with only 3 simple settings, but we will be expanding them soon
with more awesome possibilities. In order to see the settings in the UI
you can use a "cog menu":

<img src="/images/travis-settings-01.png" title="In order to get to settings pane you should click on the cog menu and choose settings" />

or a settins icon on the list of repositories in the profile:

<img src="/images/travis-settings-03.png" title="Settings link in the profile" />

It will take you to the settings pane:

<img src="/images/travis-settings-02.png" title="The look of repository settings pane" />

If you prefer using CLI just type `travis settings --help` for more info.

### New settings

At this point 3 settings are available:

* Build only commits with `.travis.yml` file - by default we build all of the commits
  pushed to GitHub, but sometimes it's not needed, branches not having `.travis.yml` file
  will most likely end up with errored out builds. By checking this option, you change
  the default behaviour to not build a commit if it does not contain a `.travis.yml`
  file.

* Build pushes - this option allows you to disable builds on pushes
* Build pull requests - this option allows you to disable builds on pull requests


We would love to hear which settings will make the most sense when moved
to the web UI for you, please let us know what you think!
