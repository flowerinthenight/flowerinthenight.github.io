---
layout: post
title: "CTO Diaries #2: Typical day"
location: "Japan"
tags: [cto-diaries, cto, diaries, startup]
---

Hi. It’s been a year since my last「CTO diaries」post. Never mind the excuses, there’s a lot.

Anyway, so what does my typical, or normal day, look like? Well, I usually start the day with checking the overall health of our systems. We don’t really have very sophisticated monitoring and alerting systems at this point so this means checking on several areas such as our Kubernetes clusters, databases, and critical services. On top of my head, I think the most common service crashes I noticed so far are OOM-related.

I also check our month-to-date infrastructure spending. We use bits of the three (AWS, GCP, and Azure). I don’t really do this meticulously; more like checking for anomalies. We’ve been hacked several times in the past for mining and these usually show up as cost anomalies. I can also keep an eye on unpredictable usages such as data transfers. Our runway is one of the many things in my list of concerns so I’d like to keep an eye on runaway costs as much as I can.

A huge chunk of the day is spent doing admin tasks. In our current phase, I’m actually more of an engineering manager than a CTO. I take part in daily standups, backlog grooming, dealing with developer blockers, schedules and priorities, interfacing with technical support, product, and customer success teams. While these are fairly straightforward, I would say that the additional overhead of “context-switching” between Japanese and English is surprisingly high, at least for me. The constant worry of whether I was able to communicate what I wanted to communicate, and all the nuances that come with that, is always there. Writing on top of verbal communication always helps.

Then 1-on-1’s. It’s not daily but it takes a huge amount of my time and energy. It’s not really that bad overall but it’s probably the most exhausting, personally. Dealing with people, with different personalities, is always a challenge, both at work and outside. I’m not a people-person really; my EQ leaves a lot to be desired. But I like to think that I’m getting good at it though.

Another part of my typical day is reading. Anything that I deem beneficial really; technical articles and papers, new developments in technology that are related to our domain, applied psychology — interestingly, business and startups, the lot. I would say this is probably the part I enjoy the most.

Last is coding, which I usually do during the wee hours of the night. Not core codebase though, mind, but support code such as tooling, CI/CD, and scaling. This is probably out of necessity more than anything. I don’t really enjoy coding that much anymore, even before I became CTO but we still can’t afford domain experts at the moment so I contribute as much as I can.

I’ll probably write about the other bits like participating in investor meetings, sync-ups with other executives, etc. on a separate post.

Alright, that's it. See you in the next one.
