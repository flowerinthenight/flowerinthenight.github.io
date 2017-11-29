---
layout: post
title: "Using glog together with cobra in golang"
location: "Japan"
tags: [golang, glog, cobra]
comments: true
---

{% gist 221e26cea495e5adc3ae6a323b4fbdba %}


{% highlight shell %}
Use glog with cobra.

Usage:
   [flags]

Flags:
      --alsologtostderr                  log to standard error as well as files
      --echo string                      echo string (default "hello")
      --log_backtrace_at traceLocation   when logging hits line file:N, emit a stack trace (default :0)
      --log_dir string                   If non-empty, write log files in this directory
      --logtostderr                      log to standard error instead of files
      --stderrthreshold severity         logs at or above this threshold go to stderr (default 2)
  -v, --v Level                          log level for V logs
      --vmodule moduleSpec               comma-separated list of pattern=N settings for file-filtered logging
  -h, --help                             help for this command
{% endhighlight %}

{% highlight shell %}
I1129 13:49:34.166660    2138 main.go:28] echo (info): hello
W1129 13:49:34.166718    2138 main.go:29] echo (warn): hello
E1129 13:49:34.166722    2138 main.go:30] echo (error): hello
{% endhighlight %}
