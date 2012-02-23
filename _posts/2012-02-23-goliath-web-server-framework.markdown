---
layout: post
title: Goliath web server framework
---

For the [first project][project] at Hackatron we want to experiment with [Goliath][goliath], the open source version of the non-blocking (asynchronous) Ruby web server framework powering PostRank.

Goliath is a lightweight framework designed to meet the following goals: bare metal performance, Rack API and middleware support, simple configuration, fully asynchronous processing, and readable and maintainable code (read: no callbacks).

One of the coolest things about Goliath is that it makes a clever use of Ruby Fibers in conjunction with Event Machine to let developers write *normal code*, following a linear execution, running instead in an asynchronous way. This leads to more readable and maintainable code that just doesn't block.

How is it possible? Well, under the hood, each Goliath request is executed in its own fiber and all asynchronous I/O operations can transparently suspend and later resume the processing without requiring the developer to write any additional code.

[project]: http://github.com/hackatron/sveglia
[goliath]: http://postrank-labs.github.com/goliath/