---
title: "Calculating Rates using Librato Metrics' Composites"
created_at: Tue 29 Apr 2014 08:00:00 CEST
layout: post
permalink: 2014-04-29-calculate-rates-using-librato-metrics/
author: Mathias Meyer
twitter: roidrage
---
In a previous blog post, we talked about [tracking new metrics when changing existing code](http://blog.travis-ci.com/2014-04-28-changing-some-code-instrument-it/).

We added code to track cache hits and misses so that we can make better decisions on possibly improving the way we cache data to serve build status images. With these metrics in place as of yesterday, I wanted to calculate the percentage cache hit rate from these two metrics.

[Librato Metrics](https://metrics.librato.com), our metrics aggregator of choice, recently [shipped a new feature called composite metrics](http://blog.librato.com/posts/composite-metrics), allowing you to combine the values from multiple metrics series to transform them into composites. For instance, you could add up all the CPU usage values in your server cluster to a global value, or calculate the sum of all requests hitting your application by adding the different counts for status codes.

This very feature comes in handy to calculate things like rates, which can be easier for a human to parse, like in the case of cache hits and misses.

To create a new composite metrics, start by creating a new instrument, for instance using the "Correlate" tab.

![](/images/2014-04-29-new-instrument.jpg)

When you click the "Metrics Composer" button, you'll notice a new input field. There you can provide a JavaScript-based combination of functions to pull different streams of metrics and run aggregation functions on them.

Say, we want to pull out the sum of all cache hits, we provide the name of the metric and the source:

    series("status-image.cache-hit", "travis-api", {function:"sum"})

We can do the same to pull out the misses:

    series("status-image.cache-miss", "travis-api", {function:"sum"})

Now we can divide both streams to get the rate of misses:

    divide([s("status-image.cache-miss", "travis-api", {function:"sum"}),
            s("status-image.cache-hit", "travis-api", {function:"sum"})])

Note that the argument for `divide` is a single array containing both results. `s` is a short hand form for `series`.

As we hit the "Generate" button, the metric is added to the instrument. Now we have the resulting rate of misses, neat!

![](/images/2014-04-29-miss-rate.jpg)

To calculate the hit rate in percent, we can use a transformation on the stream to add some more math to the mix.

![](/images/2014-04-29-transform.jpg)

We're using `100 - (x * 100)` to transform the miss rate calculated above into a percentage hit rate.

While we're at it, the stream gets a nicer name and some basic settings for minimum value and add better labels for tooltips and the y-axis.

Here's the resulting graph:

![](/images/2014-04-29-cache-hits.jpg)

Composite metrics are rather neat to aggregate multiple metrics into a single stream and to do some extra manipulation on the data. You should check them out.

We're currently working on improving our own coverage of metrics and visualization of them, they're definitely coming in handy for that purpose.
