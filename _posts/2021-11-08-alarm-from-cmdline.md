---
layout: post
title: "Setting alarm from commandline"
location: "Japan"
tags: [alarm, cmdline, commandline, gnome, linux]
---

This is just a quick one.

Although I use [Gnome Clocks](https://wiki.gnome.org/Apps/Clocks) occassionally, most of the time I set an alarm via the commandline.

{% highlight shell %}
# OS is POP_OS!, using VLC:
$ sleep 10m && \
  cvlc ~/alarm.mp3 --play-and-exit && \
  notify-send 'alarm done'
{% endhighlight %}

