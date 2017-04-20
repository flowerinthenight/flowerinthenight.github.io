---
layout: post
title: "Using APC as FIFO queue in Windows"
location: "Japan"
categories: ["C++"]
comments: true
---

For self reference:

In this way, we can implement a FIFO queue without using explicit locking/synchronization for enqueueing/dequeueing.

{% gist 48d81f079d64dabbad7fa80928159461 %}
