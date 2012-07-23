---
layout: post
title: "DaBomb: Hackatron's project for Hackitaly at H-farm"
---

[team]: http://hackatron.github.com/about.html
[hackitaly_2012]: http://hackitaly.org/post/26704644261/programma-hackitaly-camp-ing-21-22-luglio-h-farm
[ready_steady_bang]: http://chambersjudd.com/readysteadybang
[dabomb_server]: http://github.com/hackatron/dabomb-server

Today [Hackatron team][team] is attending [Hackitaly 2012][hackitaly_2012] at H-farm.

Hackitaly is *"the first geek event Made in Italy"*, a unique event in Italy where the hacker attitude is strong but the hacker community is scattered. It's a great chance to meet people you always chat or tweet with and to have fun coding and hacking.

We developed a game for iPhone called *DaBomb*. It's a multiplayer game where two players challenge each other. After pairing with another device you and your opponent have to defuse a bomb, the fastest wins. A simple but addictive game inspired by [*Ready Steady Bang*][ready_steady_bang].

Giovanni and Matteo made the server: a Sinatra app, they used Redis as storage engine and hosted the app at Heroku. You can find source code of DaBomb server at [http://github.com/hackatron/dabomb-server][dabomb_server].

Nebil and Nicola worked on the client, the iPhone app.

Here's a screenshot of the working prototype taken from Nicola's iPad:

![DaBomb app screenshot](http://p.twimg.com/Aye_GyECUAAQ4N-.png:small)