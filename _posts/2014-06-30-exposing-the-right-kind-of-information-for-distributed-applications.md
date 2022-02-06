---
title: Exposing the right kind information in distributed systems
layout: post
author: Piotr Sarnacki
twitter: drogus
permalink: /2014-06-30-exposing-the-right-kind-of-information-in-distributed-systems
created_at: Mon 30 June 2014 13:00:00 CEST
---

When you open Travis CI in a browser, you're seeing just one of many applications
that are working together in order to bring you the best CI experience. We run 8 applications
or so (depending on how you count), so we can definitely call Travis CI a distributed system.
Distributed computing solves a lot of problems and we believe it's a proper direction for
a system like Travis CI, but it also brings a lot of tough challenges. There is no silver
bullet and distributed computing surely isn't one, choose your own poison, as they say.

One of the problems of spreading your code across different servers and applications
is efficient communication which needs a set of well-defined and well-designed
APIs. Regardless a transport layer, be it HTTP, RabbitMQ messages or some kind
of binary format, you need to specify the data you want to send and receive,
its structure and a level of abstraction.

In Travis CI we're trying to learn how to do it properly and one of the things that is
very important to us is exposing the right kind of data in the APIs. As
an example I will describe one of the changes we've introduced, ability
to use encrypted environment variables on some of the pull requests.

Travis CI allows you to encrypt some of the environment
variables in order to safely store sensitive data in .travis.yml file.
For security reasons we can't decrypt such variables for some of the pull
requests, otherwise an attacker could create a pull request with a `printenv`
instruction and display all of the sensitive data. In the beginning we didn't
allow encrypted variables on any pull requests, but after a while we wanted to improve
it a little bit. If a pull request is created from a local branch, we can safely
decrypt config, because in order to create a branch you need to have push
access to the repository.

The problem was that while I were introducing the original change, I implemented
secure env check on our worker machines in a following way ([code on github](https://github.com/travis-ci/travis-build/blob/16d4860/lib/travis/build/data/env.rb#L51-L53)):

```ruby
def secure_env_vars?
  !pull_request && config_vars.any?(&:secure?)
end
```

As you may see I'm checking if a build is not a pull request. Similar logic was
introduced on our backend servers. If we treat a worker machine as a client,
this is a bad API design, because instead of consuming a high level information, a client
reimplements server's logic using lower level data. Because of that implementation
I couldn't just change a value on the server, I needed to update both sides.

The obvious improvement was to introduce a higher level information in the API, namely
`secure_env_enabled?` field. This is an implementation on the backend ([code on github](https://github.com/travis-ci/travis-core/blob/d836d0a045753a66fdc527db47d093703c7bec04/lib/travis/model/build.rb#L176-L178)):

```ruby
def secure_env_enabled?
  !pull_request? || same_repo_pull_request?
end
```

We enable encrypted env vars if a build is not a pull request or if it comes
from the same repository.

Now we can just consume a value the server sends to the worker ([code on github](https://github.com/travis-ci/travis-build/blob/master/lib/travis/build/data.rb#L83-L85)):

```ruby
def secure_env_enabled?
  job[:secure_env_enabled]
end
```

We don't rely on the lower level data anymore, instead we use whatever logic sits on the
server. Changing the conditions of enabling secure environment variables
requires change only on the server, whereas the older code required changes
both on the backend and on the worker machines (which was especially painful, our tools
to update workers where not ideal at that point).

If you're into OOP design you can quickly spot the similarity to good OOP practices.
The difference is that with a badly designed API in the boundaries of a single code
base it's usually a matter of changing a bit more code. With distributed architecture
it may mean changing several codebases and deploying the same logic change several
times. In simple words, the pain of badly designed APIs is much bigger in distributed
environments.

It's certainly hard to design API which never requires changes in more than one app,
but with some planning it is certainly possible to minimize such situations.
Whenever you add a new feature to your distributed application, think where to put
the logic. Can it be pushed upstream? Can you make clients dumb? How many applications
will you need to change if the logic changes? Asking these questions may just
save you tons of additional work and unneeded deployments and I can't stress enough
how important is to keep the scope of changes small in distributed systems.
