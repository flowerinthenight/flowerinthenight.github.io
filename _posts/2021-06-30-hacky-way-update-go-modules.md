---
layout: post
title: "A hacky way to update problematic Go modules"
location: "Japan"
tags: [golang, modules, update]
---

The only options for updating modules that I'm aware so far are a) `go get -u all`, and b) specific modules, i.e. `go get -u domain.com/module[@v1.2.3]`. For problematic ones, my only option is b), which is a bit time consuming. There must some other way out there that I'm not aware of but at the moment, I use this simple command:

{% highlight shell %}
$ cat go.mod | grep -i 'github' | grep -i -v 'indirect' | awk '{print $1}' > update; \
  while read -r v; do go get -u $v; done < update; rm update
{% endhighlight %}
