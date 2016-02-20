---
author: abualsamid
comments: true
date: 2014-12-11 01:20:02+00:00
layout: post
slug: hello-world
title: To Node or to Go
wordpress_id: 1
categories:
- Go
- Node
---

The recent news of [trouble in node](http://www.wired.com/2014/12/io-js/) land is unsettling. Nodejs is am amazing technology with a big following. Companies such as Linked-In bought into it from the early beginning. Microsoft is making it a first class citizen in the Visual Studio eco system. AWS just launched a new [service](http://aws.amazon.com/lambda/) based on node, and has a great sdk for it. [Joyent](http://www.joyent.com/) has embraced it from the get go and is now the corporate sponsor.  This is just a small set of nodejs related projects and companies, the list is huge.

We use nodejs for our home grown development tracking and management system and we are currently in the process of building out micro services to support our ever growing [SaaS offering](http://www.estratex.com/). Up till now the plan was to build out those micro services in nodejs. Now, being micro services, they do not really need to be all written in a single language. Especially those days with [Docker](https://www.docker.com/) taking over the world, it is very easy to develop different services in different technologies.

None the less, we would like to know that we have a goto option for a micro service build out, that we made a strategic decision to commit to a direction. Up till few days ago, that direction was Nodejs.

We have not changed our minds yet, Nodejs is not going away, and it still supported by a strong backer and if good things happen the rift will be healed and the community will come back together and keep pushing it forward.

However, we are now considering other options. One of the things that we have considered seriously is Google's [Go](http://golang.org/). It is a beautiful language, statically linked, so it is perfect for Docker deployment. It is supported by Google and has a ton of packages. What it does not have, yet, is an official AWS SDK from Amazon. That's really the main reason that tilted the scale in favor of nodejs, up till now.

Now, it is decision time, to Node || to Go

cross blogged on [stratex.com/blog](http://stratex.com/blog)
