---
layout: post
title: "IRC channel topic HTTP API using Hubot"
---

[hubot]: http://hubot.github.com/
[freenode]: http://freenode.net/
[irc-script]: https://github.com/hackatron/hackatron-hubot/blob/master/scripts/irc-topic.coffee
[topic-event]: https://github.com/martynsmith/node-irc/blob/master/lib/irc.js#L383
[hackatron-script]: https://github.com/hackatron/hackatron.github.com/commit/4c95643d6ecaec3484f7ea157a3e52339997fd74
[jsonp]: http://en.wikipedia.org/wiki/JSONP

Hackatron's team largely uses IRC to stay connected, we use it also to track next meetings schedules: the topic of #hackatron channel is set to something like *"Next HCKTRN 7:00 pm, 01/29 @ Meme Coworking"* so everybody who joins the chat room is always updated about our next meeting.

There's a little drawback about this way of setting next meetings schedules: it can't be shared easily. We don't want to create a new Facebook event for every meeting but we'd like also an easy way to put it on [http://hackatron.org](http://hackatron.org) so even who doesn't like to connect through IRC can be updated about next Hackatron event.

Basically we'd like to access IRC channel topic through HTTP so I can show next event informations using Javascript but [freenode][freenode] hasn't a HTTP API so how can we achieve this?

Here's where [Hubot][hubot], a chat bot developed originally at GitHub, comes to the rescue! We're using it at #hackatron channel, his name is *Hackabot*, it's a useful tool and it's been an interesting topic to work on.

Giovanni made a [script][irc-script] to access this data using a public API which responds to HTTP requests. The script adds an IRC listener to `topic` [event][topic-event] which stores inside robot's brain the channel topic, and a HTTP listener to `/hubot/topic/:channel` which responds to GET requests with a Javascript function call wrapped around the selected channel topic.

The API responds with `application/javascript` content because it uses the [JSONP][jsonp] communication technique, this way Giovanni simply put [a little script][hackatron-script] in Hackatron static site to get the result dynamically.

Now we can finally say: *get info about our next meeting at [http://hackatron.org](http://hackatron.org#next_meeting)*, or as usual by joining #hackatron at irc.freenode.net.