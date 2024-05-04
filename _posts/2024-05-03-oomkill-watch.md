---
layout: post
title: "oomkill-watch - A tool to watch OOMKilled events in k8s"
location: "Japan"
tags: [k8s, oomkilled, events, watch, kubectl, golang]
---

I recently uploaded a tool to GitHub that wraps `kubectl get events -w` command for watching `OOMKilled` events in Kubernetes. It's called [`oomkill-watch`](https://github.com/flowerinthenight/oomkill-watch). You can check out the code [here](https://github.com/flowerinthenight/oomkill-watch). You might find this useful.
