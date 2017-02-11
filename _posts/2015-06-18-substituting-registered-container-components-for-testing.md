---
layout: post-no-feature
title: "Substituting registered container components for testing"
category: articles
tags: [post, readability, test]
---
I want to test my services end-to-end. I want to guarantee I'm testing behaviour and not implementation. I do not want my tests to be brittle and I want to refactor. I want to test that my container registration conventions work. I want my tests to run in milliseconds not seconds, be repeatable and not dependent upon physical infrastructure such as persisted state, or items on a queue. I need my tests to run in-memory only. My code is persistence ignorant. So I need to substitute my persistent data-store with in-memory testing implementations.

How do I substitute container components already registered by convention with my in-memory implementations? Without making changes to the production code?

I have created a simple Windsor facility that is only averrable to the test assembly. When resolving pre-configured container components it substitues them.

Here is an example, whereby a [bootstrapped](https://gist.github.com/blazey/b959af307923eebae028#file-bootstrap-cs) container has components substituted in a test: 

<script src="https://gist.github.com/blazey/9c7cc7b6bcb276142d5e.js"></script>

Now the components that use a service bus, hanger.io, hbase or persistent store are substituted with appropriate test doubles like a mock, stub, or in-memory store. I can now test the behaviour of the service without bastardising my container conventions to substitute components that are expensive and superfluous to the [SUT](http://xunitpatterns.com/SUT.htm).

And here is the first stab at my implementation: 

<script src="https://gist.github.com/blazey/646b2e90e9454d827fd4.js"></script>