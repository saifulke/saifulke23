---
title: "Changing Some Code? Instrument It!"
author: Mathias Meyer
twitter: roidrage
created_at: Mon 28 Apr 2014 12:00:00 CEST
permalink: 2014-04-28-changing-some-code-instrument-it
layout: post
---
Legacy code can be problematic to handle, both from the perspective of testing and from keeping it running in production.

For adding tests to an existing code base, there's a good rule of thumb to increase test coverage, slowly but surely.

Whenever you change some of the existing code, write tests for it. Every new tests adds to the overall confidence of making more changes over time.

Legacy code often suffers from another problem: lack of coverage in terms of metrics, in terms of monitoring.

Why not apply the same approach here then?

**Whenever you touch code that's not instrumented, add metrics.** Whenever you touch code that broke in production but hasn't given you enough insight when it did, add logging.

Last week we had a short outage of our API because the Memcached server was temporarily unavailable. It recovered after a few minutes, but until then, the API failed miserably because about 1/3 of the requests we get touch Memcached. But the code doesn't handle failures gracefully.

These requests touch Memcached to check for the last status for a repository, to deliver the right build status image based on branch and build result. We store these results in Memcached as the builds finish.

The code in question doesn't need to let errors bubble to the top. It can just as well resort to using the database if need be, handling the request much more gracefully. Alternatively, it could also return an static result to reduce the impact on the database when the cache isn't available.

Either way, the code now tracks when an error occurs. We retry Memcached requests, but eventually they'll fail in scenarios when the server is fully unavailable.

Additionally, I realized that we don't track any data on cache hits and misses. So I added the right metrics to track them to the code. Let's look at an example, our code to fetch data for the build status badges from the cache. Here's the old code:

{% highlight ruby %}
def state_from_cache
  return unless repo
  return unless cache_enabled?

  cache.fetch_state(repo.id, branch)
end
{% endhighlight %}

It does a few checks and then hits the cache to fetch the data. Simple enough to [add a metric to track hits and misses](https://github.com/travis-ci/travis-core/blob/482f201257f29176497415711d99c3cbd230072f/lib/travis/model/repository/status_image.rb#L30-L44):

{% highlight ruby %}
def state_from_cache
  return unless repo
  return unless cache_enabled?

  cache.fetch_state(repo.id, branch).tap do |result|
    if result
      Metriks.meter('status-image.cache-hit').mark
    else
      Metriks.meter('status-image.cache-miss').mark
    end
  end
end
{% endhighlight %}

On top of that, [errors in the cache are also tracked and handled
better](https://github.com/travis-ci/travis-core/blob/482f201257f29176497415711d99c3cbd230072f/lib/travis/states_cache.rb#L107-L123).

What used to bubble up errors from the underlying library, now handles them better and raises a more specific error message. Plus, it tracks a metric for every error that we can now alert on, if it reaches a certain threshold.

    
{% highlight ruby %}
def get(key)
  retry_ringerror do
    pool.with { |client| client.get(key) }
  end
rescue Dalli::RingError => e
  Metriks.meter("memcached.connect-errors").mark
  raise CacheError,
        "Couldn't connect to a memcached server: #{e.message}"
end
{% endhighlight %}

Last week's outage benefitted our monitoring in two ways.

A Memcached outage doesn't impact the entire API anymore. It also doesn't dump stacktraces all over the logs, just simple error messages. Based on the metrics, we can set up alerts.

But what's more, we can now make better decisions on how our status image data is cached and accessed.

Changing uninstrumented code is an opportunity to improve coverage of the metrics you're tracking for your app. Use it, it's mostly just one or two lines of code! Little investment, great long term return.
