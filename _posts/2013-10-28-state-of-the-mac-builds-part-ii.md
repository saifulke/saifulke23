---
title: "State of the Mac Builds – Part II"
created_at: Mon 28 Oct 2013 20:00:00 CET
author: Henrik Hodne
twitter: henrikhodne
layout: post
permalink: /2013-10-28-state-of-the-mac-builds-part-ii
---

Hello again! [A few weeks back](/2013-09-27-state-of-the-mac-builds/)
we blogged about the state of the Mac cloud, and mentioned about working to get
iOS 7 and Xcode 5 up and running. I'd like to take a moment to review what we
have been working on lately and how we're working on getting this live for you
to use.

When we first started to work on the upgrade to Xcode 5, we realized that we
had to update OS X as well as Xcode, since Xcode 5 requires at least OS X
10.8.4, and we were still running OS X 10.8.2. While we were working with
[Sauce Labs](https://saucelabs.com), our Mac infrastructure provider, to update
to 10.8.4, we also decided to switch to their new virtualization platform. This
would make the Mac cloud faster, more stable and the process of updating to
10.8.4 easier.

We expect Xcode 5 and iOS 7 support to be live in the Travis cloud no later
than Thursday November 7th, if not sooner.

We are very sorry for the extended delay in providing Xcode 5 and iOS 7 testing
to you. While working on this update we have also been working on ways to get
these updates live much faster in the future.

A quick note on OS X Mavericks, which was also released recently: We plan to
support OS X Mavericks, and will start working on updating to OS X Mavericks as
soon as we have Xcode 5 and iOS 7 testing live.

**Update**: We are working with our infrastructure partner Sauce Labs on the
final stages of bringing the Mac cloud up, including the configuration of the
API and testing the updated OSX image. Due to this, the upgrade to Xcode 5 and
iOS 7 has been delayed until tomorrow, Friday November 8th. We're very sorry
for this additional delay and will update the blog as soon as we have more
news.

**Update II**: We are continuing to work with our infrastructure partner on the
update. The setup is taking longer than expected, we anticipate the update to
be finished over the weekend.
