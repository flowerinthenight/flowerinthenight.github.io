---
layout: post
title: "Download the latest Github release using command line"
location: "Japan"
tags: [cmdline, download, github, release]
---

_For personal reference:_

Download the latest GitHub Releases asset using common command line tools:

{% highlight shell %}
# Update the url accordingly.
# The `uname | awk` subcmds will output 'Linux'|'Darwin'.
$ curl -s https://api.github.com/repos/alphauslabs/bluectl/releases/latest | \
  jq -r ".assets[] | select(.name | contains(\"$(uname -s | awk '{print tolower($0)}')\")) | .browser_download_url" | \
  wget -i -
{% endhighlight %}
