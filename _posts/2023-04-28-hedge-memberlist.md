---
layout: post
title: "Attempt to replace hedge's member tracking with hashicorp/memberlist"
location: "Japan"
tags: [memberlist, hedge, distributed-computing]
---

I recently came across [hashicorp/memberlist](https://github.com/hashicorp/memberlist) library while browsing GitHub and I thought it would be a good replacement for [hedge](https://github.com/flowerinthenight/hedge)'s internal member tracking logic. It seems to be widely used (thus more battle-tested) as well. I was quite excited as I always thought that hedge's equivalent logic is too barebones and untested outside of our use cases. It works just fine for its current intended purpose but I've been hesitating to build on top of it until I can really say that it's stable enough. With memberlist, it might just be what I needed.

After about a month of testing, I think it didn't really turn out well in the end. It is stable enough for deployments that are not spike-y in terms of workloads (frequent scaling up/down). Or if I set min = max in the HorizontalPodAutoscaler. In these cases, memberlist can consistently track members just fine. What's better is that it works even in multiple deployments in the same namespace which I thought was brilliant. For example, if I have a deployment `app1` set to 10 pods in the `default` namespace using memberlist's default port numbers, and then I deploy another set, say, `app2`, within the same namespace using the same ports, app1's memberlist can track its 10 member pods just find while app2's memberlist is also separated. But when applied to my use case, which has a minimum pod of 2 and a max of 150, with frequent scale up/down frequency depending on load, it can't seem to keep up. The potential for [Byzantine faults](https://en.wikipedia.org/wiki/Byzantine_fault) is just too high: i.e. in a 50-pod scale, memberlist can end up having 2 groups of m-pods and n-pods where m+n=50. Very rarely, it can even go up to 3 groups.

I was quite frustrated. I really wanted it to work; I even attempted to update memberlist to incorporate hedge's logic but it was too much for now, with my schedule. So now, back to the old one. By the way, the current logic is fairly rudimentary: all members in the cluster/group send a liveness heartbeat to the leader and the leader broadcasting the final list of members to all via hedge's broadcast mechanism. CPU usage between the two is fairly similar depending on the sync timeout.

I've been trying to improve hedge's member tracking system as I want to build a distributed in-memory cache within hedge itself. Most of the available ones are [Raft](https://raft.github.io/)-based, and I still haven't figured out how to make Raft work in the same deployment configuration.
