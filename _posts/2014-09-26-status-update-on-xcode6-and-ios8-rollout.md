---
title: "Status update on the Xcode 6 and iOS 8 rollout"
author: Henrik Hodne
twitter: henrikhodne
created_at: Fri 26 Sep 2014 17:20:00 UTC
layout: post
permalink: 2014-09-26-status-update-on-xcode6-and-ios8-rollout
---

**Update: We rolled out the Xcode 6 update two weeks ago, but saw some issues after rolling it out. The majority of these issues have been fixed, see the [status page](http://status.travis-ci.com/incidents/y9pysslbxb79) for more information. A postmortem will be published on Wednesday, October 22nd, which will detail the problems we encountered with the update, as well as improvements we will be making to the update process.**

It's been nine days since Xcode 6 was released, and I wanted to give you an update on what we've been doing to get it rolled out to you.

We started working on this as soon as Xcode 6 was out, but had some issues booting up and connecting to the base VM that we use to install any updates. Once we got the machine booted up and got past the connection issue (turned out to be a bug in the VPN client that I use), we started updating the software in the build environment.

Our first attempt at rolling this out was on September 24th. Once we enabled the new image, we almost immediately started getting errors. We rolled back to the old image and started investigating the source of the errors. We found that the image had disappeared from the VM hosts. This meant that we had to re-distribute the image from the master image again. Due to the length of this process, this meant that we were unable to try again until the next day.

Our second attempt at rolling out the image was yesterday, September 25th. We verified that the image was on all the VM hosts this time, and flipped the switch to use the new image. This time the VMs were booting up, but pretty soon we started seeing timeout errors when SSHing into the machines. We tried looking at the screens over VNC and discovered that the machines were getting stuck in the boot sequence, and some asked for a password (even though we have passwordless login enabled).

We're still trying to figure out the booting issue with our infrastructure team, and we hope to have this resolved as soon as possible.

I'm really sorry for the delays in getting this update out to you.
