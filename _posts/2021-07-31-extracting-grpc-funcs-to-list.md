---
layout: post
title: "Extract gRPC-generated functions to a list"
location: "Japan"
tags: [golang, grpc, grpc-gateway, cmdline]
---

This might be hacky and there might a proper way to do this but recently, I needed to generate all the functions' gRPC-generated full names from our protobuf definitions. This was part of our RBAC module that needs to filter gRPC function calls. I got the list from our [generated Go client](https://github.com/alphauslabs/blue-sdk-go) using the following command(s):

{% highlight shell %}
# Main command:
$ grep -o -R -i -E '"/blueapi\..*"' . | awk -F':' '{gsub(/"/, "", $2); print "-", substr($2, 2);}' | sort | uniq

# Actual commands; save as yaml:
$ echo "functions:" > /tmp/funcs.yaml
$ grep -o -R -i -E '"/blueapi\..*"' . | awk -F':' '{gsub(/"/, "", $2); print "-", substr($2, 2);}' | \
  sort | uniq >> /tmp/funcs.yaml
{% endhighlight %}

The final results are now uploaded to this [repository](https://github.com/alphauslabs/blueapi-functions).

