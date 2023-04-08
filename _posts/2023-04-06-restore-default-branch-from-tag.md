---
layout: post
title: "Restore default branch from tag while preserving history"
location: "Japan"
tags: [git, history]
---

Fore self reference:

To restore default branch from a tag while preserving history, do:

{% highlight shell %}
$ git checkout tags/v1.2.3 -b v1.2.3
$ git diff main > /tmp/diff.patch
$ git checkout main
$ cat /tmp/diff.patch | git apply
$ git commit -am "Rolled back to v1.2.3"
$ git push origin main
{% endhighlight %}
