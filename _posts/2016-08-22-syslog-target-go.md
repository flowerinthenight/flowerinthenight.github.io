---
layout: post
title: "Syslog as target in Go logs"
location: "Japan"
categories: ["Code", "golang"]
comments: true
---

For personal reference:

{% highlight go %}
package main

import (
    "log"
    "log/syslog"
    "os"
)

func main() {
    trace, err := syslog.New(syslog.LOG_INFO, "myapp")
    if err != nil {
	    log.Println("Cannot open syslog. Terminate.")
	    os.Exit(-1)
    }

    defer func() {
	    log.Println("Closing myapp.")
	    trace.Close()
    }()

    log.SetFlags(log.Ldate | log.Ltime | log.Lshortfile)
    log.SetOutput(trace)

    log.Println("Hello world!")
}
{% endhighlight %}

To view syslogs

{% highlight shell %}
tail -f /var/log/syslog
{% endhighlight %}
