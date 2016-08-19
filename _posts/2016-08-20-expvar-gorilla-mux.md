---
layout: post
title: "How to serve expvar when using gorilla/mux"
location: "Japan"
categories: ["Code", "golang"]
comments: true
---

For personal reference:

{% highlight go %}
package main

import (
    "expvar"
    "log"
    "net/http"

    "github.com/gorilla/mux"
)

var counter *expvar.Int

func init() {
    counter = expvar.NewInt("counter")
}

func rootHandler(w http.ResponseWriter, r *http.Request) {
    w.Write([]byte("Hello world!\n"))
    counter.Add(1)
}

func main() {
    r := mux.NewRouter()
    r.HandleFunc("/", rootHandler)
    r.Handle("/debug/vars", http.DefaultServeMux)
    log.Fatal(http.ListenAndServe(":8000", r))
}
{% endhighlight %}

### Access root

{% highlight shell %}
http://localhost:8000
{% endhighlight %}


### Access expvars

{% highlight shell %}
http://localhost:8000/debug/vars
{% endhighlight %}
