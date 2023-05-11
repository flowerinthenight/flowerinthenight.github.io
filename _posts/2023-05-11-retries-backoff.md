---
layout: post
title: "Retries with backoff in distributed systems"
location: "Japan"
tags: [retry, retries, backoff, distributed-systems]
---

In a distributed system, where multiple processes communicate with each other over a network, failures are inevitable. Network partitions, hardware failures, and software bugs can all cause a request to fail. Retries with backoff are a critical technique to help mitigate these failures.

Retries refer to the act of retrying a failed request. When a request fails, the client can retry the request, hoping that it will succeed the next time around. However, simply retrying the request immediately after a failure can be problematic. If the failure was caused by a temporary network issue, for example, retrying immediately will likely result in another failure. This is where backoff comes in.

Backoff refers to the practice of waiting a certain amount of time before retrying a failed request. The idea is to wait long enough for any temporary issues to resolve themselves before retrying. The amount of time to wait is typically increased with each retry, hence the term "backoff." The idea is that if the request fails multiple times, the client will eventually back off enough to give the system a chance to recover.

There are several benefits to using retries with backoff in a distributed system. First, it can help reduce the impact of temporary failures. By waiting before retrying a request, the caller can avoid bombarding the target with requests, which can exacerbate the problem. Second, it can help improve overall system availability. By retrying failed requests, the caller can work around transient issues that might otherwise cause the entire system to fail.

There are several strategies for implementing retries with backoff. One common approach is exponential backoff, where the client waits an increasing amount of time between each retry. Another approach is jittered backoff, where the client adds a random amount of time to the wait period to avoid the so-called "thundering herd" problem, where multiple clients all retry at the same time.

Example 1:

{% gist ec8a4a833e039bed8b13552dbad5f9b5 %}

Example 2 (my preference):

{% gist 33bbe6d25e7794db471c105cc40e63dd %}

In conclusion, retries with backoff are an important technique for improving the robustness and availability of distributed systems. By waiting before retrying failed requests, the client can help reduce the impact of temporary failures and improve overall system availability. There are several strategies for implementing retries with backoff, and choosing the right approach will depend on the specific requirements of the system.
