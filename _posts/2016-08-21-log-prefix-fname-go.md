---
layout: post
title: "Add function name prefix to log.Println in Go (golang)"
location: "Japan"
categories: ["Code", "golang"]
comments: true
---

For personal reference:

{% highlight go %}
package main

import (
    "fmt"
    "log"
    "regexp"
    "runtime"
)

func traceln(v ...interface{}) {
    pc, _, _, _ := runtime.Caller(1)
    fn := runtime.FuncForPC(pc)
    fno := regexp.MustCompile(`^.*\.(.*)$`)
    fnName := fno.ReplaceAllString(fn.Name(), "$1")
    m := fmt.Sprintln(v...)
    log.Println("["+fnName+"]", m)
}

func main() {
    traceln("Hello world!", 100, true, nil)
}
{% endhighlight %}
