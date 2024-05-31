---
layout: post
title: "memx - Get process' memory usage (Linux)"
location: "Japan"
tags: [process, memory, usage, linux, golang]
---

I shared a simple piece of code for getting a process' memory usage in Linux. It's called [`memx`](https://github.com/flowerinthenight/memx). I've used this piece of code many times at work. We use memory-mapped files extensively in some of our services and this is how we get more accurate results. Very useful in debugging `OOMKilled` events in k8s.
