---
layout: post
title: All you need is... a Docker Container
description: Cristian and Nicola want to draw the attention to a new tool for software development and production introducing Docker container.
---

Is it really necessary a whole VM for your workflow development needs ? Or all you need is a bounce of Applications ?

Containers exist from a long time, and they isolate applications, creating a read-write layer over a read-only file system.
[Docker](https://www.docker.com/) makes these things very simple.

Containers can be linked together, share volumes data, ports and services in a simple way, 
so you can prepare and share in a team, a full stack of applications for running your app!

Applications inside a container need only files from an image and they run (nearly natively) fast.
Also it's very easy to create and destroy containers so you can adapt your enviroment.

Don't have your attention? 
Let's try this

`sudo docker run -t -i ubuntu:14.04 /bin/bash`

A [set of slide](http://hackatron.org/slides/all_you_need_is_a_docker_container.html#/) has been made for an introduction that we hope can stimulate your curiosity.

We invite you to try this new software, test it in your abitual configuration, and share your experience!

Resources:

<iframe width="560" height="315" src="//www.youtube.com/embed/CyCnPwVL4RQ" frameborder="0" allowfullscreen></iframe>
