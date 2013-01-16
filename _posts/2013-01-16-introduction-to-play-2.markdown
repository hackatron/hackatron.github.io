---
layout: post
title: "Meeting[0]: Introduction to Play 2"
---


Yesterday we met for our first meeting. Matteo Depalo's duty was to introduce Hackatron to the Play 2 Framework.

He prepared a presentation about the history of Scala, Play 2 and a brief overview about Promises and Futures and how to use them in order to produce an asynchronous HTTP request.

### Scala

Scala is a language created by Martin Odersky in 2004. It's based on Java and it's inspited by the most important functional languages such as Haskell and Elang and also by Smalltalk. Scala is both functional and OO and here it lies its true power.

### Play 2

Play 2 is a web framework released in 2012, built with Scala and inspired by modern web frameworks such as Rails and Django.

The feature that stands out the most is possibility to handle asynchronous non-blocking requests out of the box. This is great for streaming and for heavy computational operations that need to be run in a separate thread without blocking the entire web server.

### Akka

Akka is the Scala actor library. Its Future and Promise objects are used to encapsulate computations that need to be run on a separate thread. These objects are now merged in the core Scala language as of v2.10 so the Play 2.1 is having a big rewrite of Future and Promises APIs.

The presentation is available [here](http://www.slideshare.net/MatteoDepalo/play-2-introduction)