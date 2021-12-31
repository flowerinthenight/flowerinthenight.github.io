---
layout: post
title: "Support the 'Any' protobuf type from an external grpc-gateway process"
location: "Japan"
tags: [protobuf, grpc-gateway, any]
---

This is just a quick one.

I had some trouble making the [`Any`](https://developers.google.com/protocol-buffers/docs/proto3#any) protobuf type work when running [`grpc-gateway`](https://github.com/grpc-ecosystem/grpc-gateway) from a separate process with the gateway throwing an unknown message type error. A quick fix for this is to import the generated `pb.go` file to your proxy source. Something like:

{% highlight go %}
package main

import (
    ...

    _ "github.com/username/pkgwithpbgo"
)
{% endhighlight %}
