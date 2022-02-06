---
title: "New API Docs and Deprecation"
created_at: Tue 30 Apr 2014 18:00:00 CEST
layout: post
permalink: 2014-04-30-new-api-docs/
author: Konstantin Haase
twitter: konstantinhaase
---

Today we have three announcements to make: We have rewritten our [API documentation](http://docs.travis-ci.com/api/), we are deprecating version 1 of our API and we will require the `User-Agent` header to be set for all requests.

## New API Documentation

Exciting news: We have completely rewritten our [API documentation](http://docs.travis-ci.com/api/). All the endpoints and payloads are now documented and there are examples for accessing them via HTTP directly, via our command line client and via our Ruby library.

<figure>
  [ ![The new API docs.](/images/api_docs.png) ](/images/api_docs.png)
  <figcaption>The new API docs.</figcaption>
</figure>

We are using [TripIt's Slate](https://github.com/tripit/slate) as a template. It makes a great boilerplate for API documentation. We'd also like to thank [Thais Camilo](https://twitter.com/narwen) for her help with writing the docs.

## Deprecating Version 1

Right now, our API serves version 1 of our payloads if it is available. If not, it chooses version 2 instead. The latter is also the format used by our [Ember.js client](https://github.com/travis-ci/travis-web).

This leaves API responses in a very inconsistent state. Moreover, version 1 is not maintained.

To give you an idea what we're talking about, the version 1 payload for [Sinatra](https://github.com/sinatra/sinatra) looks like the following:

    {
      "id": 82,
      "slug": "sinatra/sinatra",
      "description": "Classy web-development dressed in a DSL",
      "public_key": "-----BEGIN RSA PUBLIC KEY----- ...",
      "last_build_id": 23436881,
      "last_build_number": "792",
      "last_build_status": 1,
      "last_build_result": 1,
      "last_build_duration": 2542,
      "last_build_language": null,
      "last_build_started_at": "2014-04-21T15:27:14Z",
      "last_build_finished_at": "2014-04-21T15:40:04Z"
    }

Compare that to version 2:

    {
      "repo": {
        "id": 82,
        "slug": "sinatra/sinatra",
        "description": "Classy web-development dressed in a DSL",
        "last_build_id": 23436881,
        "last_build_number": "792",
        "last_build_state": "failed",
        "last_build_duration": 2542,
        "last_build_language": nil,
        "last_build_started_at": "2014-04-21T15:27:14Z",
        "last_build_finished_at": "2014-04-21T15:40:04Z",
        "github_language": "Ruby"
      }
    }

We will switch to serve the version 2 format for all endpoints by default on or after **July 1, 2014** and will stop serving version 1 completely on or after **September 1, 2014**.

To have all endpoints return the new format right away, set the `Accept` header to `application/vnd.travis-ci.2+json`.

## Requiring User-Agent

Starting on or after **July 1, 2014**, we will reject API requests that do not include a `User-Agent` header.

Assuming your client is called “My Client”, and it’s current version is 1.0.0, a good value would be `MyClient/1.0.0`. For our command line client running on OS X 10.9 on Ruby 2.1.1, it might look like this: `Travis/1.6.8 (Mac OS X 10.9.2 like Darwin; Ruby 2.1.1; RubyGems 2.0.14) Faraday/0.8.9 Typhoeus/0.6.7`.

Our [official Ruby client](https://github.com/travis-ci/travis.rb) will take care of both using the new payload and setting the User-Agent for you.

We hope to inspire and enable you to build and automate on top of our API. Let us know if you have any questions, feedback or projects you want to show us.
