---
layout: post
title: Sveglia's Timer model class
---

Sveglia app is composed by two main model classes: `Timer` and `TimerTemplate`, this post will explain some implementations details of `Timer` class.

`Timer` class models a countdown timer. Countdown timers can be *created*, *paused*, *resumed* and *destroyed*.

To create a timer the minimal information needed is *countdown target time*: the precise time at which timer will end. This information is stored in `target_at` attribute.

A mandatory requirement: *timers must accumulate pause time durations* to track the *total pause time duration*. Here are a couple ways to handle this task.

### `paused_for` and `paused_at`

Using an accumulator: `paused_for`. Its initial value is set to `nil` and it's updated at every *resume event* adding the result of `Time.now` - `paused_at` to current value.

### `origin_target_at`

The `origin_target_at` is set at creation time with original `target_at` attribute's value. At the end of timer total pause time duration is the result of `target_at` - `origin_target_at`.

This way to handle *pause time durations accumulation* is more efficient because it doesn't involve the *n* operations to add each *i<sup>th</sup> pause duration* used by `paused_for` accumulation.

### Life cycle

To summarize a timer's life cycle below are described steps involving in each timer event: *creation*, *pause*, *resume* and *end*.

When you *create* a new timer:

 * `target_at` and `origin_target_at` are set to timer's *end time*,
 * `created_at` is set to `Time.now`,
 * `paused_at` is set to `nil`.

When you *pause* a running timer:

 * `paused_at` attribute is updated with `Time.now` value.

When you *resume* a paused timer:

 * `paused_at` attribute is set to `nil`,
 * `target_at` attribute is updated with result of `Time.now` - `paused_at`.

When a timer *ends*:

 * *total pause time duration* dynamic attribute is the result of `target_at` - `origin_target_at`.