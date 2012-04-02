---
layout: post
title: Assets management with Sprockets on Goliath
---

At Hackatron we're working on a project based on Goliath, an open source version of the non-blocking (asynchronous) Ruby web server framework powering PostRank.

Goliath is great at serving APIs, but what's the most clever way to consume that API?

We decided to use a javascript framework to build an heavy client to interact with the API and we choose [Backbone.js][backbone] to achieve this goal.

We love its simplicity and its REST compliance but you must include a lot of javascript files in your pages. This could degrade performances due to an high number of requests, but it's also a pain for developers when you must add a new `script` tag for every new piece of software you're developing. A simple workaround is to put them all in one big file but this is not a real solution, it's ugly and we won't do it this way.

A clever way to include a lot of javascripts and stylesheets in your web app is to make it using [Sprockets][sprockets].

Sprockets is a Ruby library for compiling and serving web assets. It features declarative dependency management for JavaScript and CSS assets, as well as a powerful preprocessor pipeline that allows you to write assets in languages like CoffeeScript, Sass, SCSS and LESS.

We've released a [draft version][draft] of this integration and hopefully we'll release soon a gem that does this for you with a couple lines of code.

Keep reading Hackatron's blog to stay up to date.

[backbone]: http://documentcloud.github.com/backbone/
[sprockets]: https://github.com/sstephenson/sprockets
[draft]: https://github.com/hackatron/sveglia/commit/cbe8925274e591c19e5bbdd9bca2928e1d11204a