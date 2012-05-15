---
layout: post
title: The making of Sveglia using Meteor
---

[quick_start]: http://docs.meteor.com/#quickstart

### Our TODO app

We tried to implement Sveglia using goliath. Thanks to Nicola we decided to experiment this framework and it was great but we needed more.

We all code Ruby professionally, at Hackatron we'd like to face with uncommon problems, we want to give a try to a new language more than a new framework.

Our first goal at Hackatron is to *learn by doing* and we want to try Meteor so why not try to build Sveglia again using Meteor?

Sveglia is a really simple app that helps focusing on the tools you're using to make it rather than on how to make it, this is why you can consider Sveglia as Hackatron's TODO app.

### Meteor

Meteor is a set of new technologies for building top-quality web apps in a fraction of the time.

It's an *ultra-simple*, *database-everywhere*, *data-on-the-wire*, *pure-Javascript* web framework.

A Meteor application is a mix of JavaScript that runs inside a client web browser, JavaScript that runs on the Meteor server inside a Node.js container, and all the supporting HTML fragments, CSS rules, and static assets.

Meteor automates the packaging and transmission of these different components. And, it is quite flexible about how you choose to structure those components in your file tree.

#### Seven Principles of Meteor

1. *Data on the Wire.* Don't send HTML over the network. Send data and let the client decide how to render it.
1. *One Language.* Write both the client and the server parts of your interface in JavaScript.
1. *Database Everywhere.* Use the same transparent API to access your database from the client or the server.
1. *Latency Compensation.* On the client, use prefetching and model simulation to make it look like you have a zero-latency connection to the database.
1. *Full Stack Reactivity.* Make realtime the default. All layers, from database to template, should make an event-driven interface available.
1. *Embrace the Ecosystem.* Meteor is open source and integrates, rather than replaces, existing open source tools and frameworks.
1. *Simplicity Equals Productivity.* The best way to make something seem simple is to have it actually be simple. Accomplish this through clean, classically beautiful APIs.

#### Installing Meteor

To get started with Meteor you should just follow the ["Quick start"][quick_start] section of Meteor docs.

We needed some extra packages so Matteo forked Meteor's git repo and added `date` and `bootstrap` packages.

**Note:** from Meteor 0.3.4 the `bootstrap` package is on the default package list but I can ensure that first author of this package was Matteo.

To install our Meteor's fork clone the repo

    $ git clone git://github.com/hackatron/meteor.git

then run

    $ cd meteor
    $ sudo install.sh

#### Create a new Meteor app

Now that our system is ready we can create a new Meteor app running

    $ meteor create sveglia

Let's run a local web server

    $ cd sveglia
    $ meteor
    Running on: http://localhost:3000/

If you have a rails app continuously running on port 3000, as we have, you can run Meteor server on a different port by specifing the `-p` option followed by an integer representing port number.

#### Models and collections

Sveglia app has three main goals:

1. create one shot countdown timers;
1. create timer templates;
1. create one shot countdown timers from timer templates.

According to this plan we built two main collections: `Timers` and `TimerTemplates`.

Each collection is respectively a set of `Timer` and `TimerTemplate` model instances.

#### Views and templates

Relying on the fifth principle of Meteor and according to Meteor conventions `Timer` and `TimerTemplate`'s templates are already binded to related models' events.

We've just added a couple of callbacks to forms submission events that create timers and timer templates, other events are handled by Meteor library which takes care of view updates.

This is part of Meteor's strenght, following Meteor's conventions you'll get a fully reactive app in just a hundred lines of code.

#### Reactivity, notifications and subscriptions

We need to update timers' expirations, the simplest way to get this task done is using the `Session` object.

`Session` provides a global object on the client that you can use to store an arbitrary set of key-value pairs.

What's special about `Session` is that it's *reactive*. If you call `Session.get('current_list')` from inside a template, the template will automatically be rerendered whenever `Session.set` is called.

We use this feature to update timers' templates seamlessly, we put `Session.get('now')` inside expiration date calculation then we just update a couple of times per second the `now` value running `Session.set('now', new Date())`, that's it.

#### Screenshot and references

A screenshot of Sveglia app running a timer.

![Sveglia screenshot](/images/timer_template_instance.png)

You can play with Sveglia online at [http://sveglia.meteor.com](http://sveglia.meteor.com) and fork the repo at [https://github.com/hackatron/sveglia-meteor](https://github.com/hackatron/sveglia-meteor).