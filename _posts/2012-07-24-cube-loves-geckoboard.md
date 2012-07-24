---
layout: post
title: "Cube loves Geckoboard"
category: statistics
tags: [statstics, cube, geckoboard, chef, ruby]
---

*This is a [guest post](http://matteodepalo.github.com/statistics/2012/07/23/cube-loves-geckoboard/) by Matteo Depalo from the Responsa team.*

## Introduction

This is a summary of my experiences and a mini-guide regarding the deploying and usage of a Cube server and Geckoboard to track statistics at Responsa.

I'll explain how I deployed Cube to a VPS in the cloud and how I've integrated it in Responsa. I'll also talk about Geckoboard and how we used it to draw graphs based on metrics extracted from Cube, but first here's a brief description of Cube and Geckoboard.

### Cube

[Cube](http://square.github.com/cube/) is a system for collecting timestamped events and deriving metrics. By collecting events rather than metrics, Cube lets you compute aggregate statistics post hoc. It also enables richer analysis, such as quantiles and histograms of arbitrary event sets.

### Geckoboard

[Geckoboard](http://www.geckoboard.com) is a service for drawing graphs and statistics and organizing them in widgets that populate dashboards.

## Deploying

To deploy the Cube server I've chosen Linode, a service that gives you an empty Ubuntu Server virtual machine in the cloud. After the creation of the machine you can just ssh inside and start installing your server.

To make the deploying process automatic I've chosen [chef](http://wiki.opscode.com/display/chef/About), and in particular [chef-solo](http://wiki.opscode.com/display/chef/Chef+Solo).
	
Since chef uses ruby we need to install it first in our machine so just run these commands to get some basic stuff:

	# git and curl
	apt-get -y update
	apt-get -y install curl git-core python-software-properties
	
	# ruby
	curl -L https://raw.github.com/fesplugas/rbenv-installer/master/bin/rbenv-installer | bash
	vim ~/.bashrc # add rbenv to the top
	. ~/.bashrc
	rbenv bootstrap-ubuntu-10-04
	rbenv install 1.9.3-p125
	rbenv global 1.9.3-p125
	gem install bundler --no-ri --no-rdoc
	rbenv rehash
	
Then you can install Cube with:

	git clone git://github.com/matteodepalo/cube.git
	cd cube

Now all you need to do is to download the cookbooks and run chef:

	gem install librarian
	librarian-chef install
	chef-solo -c solo.rb

And your Cube server should be up and running ready to track events!

## Tracking events

We use Ruby on Rails as our stack so I've chosen the [cube-ruby](https://github.com/codykrieger/cube-ruby) gem to communicate with the server. With this gem you can talk with the [Cube collector](https://github.com/square/cube/wiki/Collector) in order to track events.

For example if we want to track a request we can write:

	$cube.send "request", :value => 'somevalue'

## Analysis

To compute metrics I've created a ruby gem called [cube-evaluator](https://github.com/matteodepalo/cube-evaluator), which talks with the [Cube evaluator](https://github.com/square/cube/wiki/Collector).

Let's say we want the daily requests on our website in this month we can write:

	daily_requests = Cube::Evaluator.metric(
					   :expression => 'sum(request)',
					   :start => 1.month.ago,
					   :stop => Time.now,
					   :step => '1day'
					 )

`daily_requests` will be an Hash containing the array of times and the array of corresponding values

## Drawing

Geckoboard needs an endpoint in your server to poll in order to draw the data. To ease the creation of these endpoints I've improved and used the [chameleon gem](https://github.com/matteodepalo/chameleon). Just add it to your gemfile

	gem 'chameleon', :git => 'git://github.com/matteodepalo/chameleon.git'
	
then run bundle to install it

	bundle install
	
Let's draw the daily_requests now. Create a line widget graph

	rails g chameleon:widget requests line

and use your daily_requests hash to populate it

	Chameleon::Widget.new :requests do
	  key "3618c90ec02d5a57061ad7b78afcbb050e50b608"
	  type "line"
	  data do
	    {
	      :items => daily_requests[:values],
	      :x_axis => daily_requests[:times],
	      :y_axis => [daily_requests[:times].min, daily_requests[:times].max]
	    }
	  end
	end
	
Congrats! You are now tracking statistics in the coolest way possible ;)

