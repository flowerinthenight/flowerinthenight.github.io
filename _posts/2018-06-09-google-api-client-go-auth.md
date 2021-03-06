---
layout: post
title: "Authenticating Google API Client Library for Go using Service Accounts"
location: "Japan"
tags: [gcp, google, api, authentication, service-account]
---

This post is specifically for the autogenerated [Google APIs Client for Go](https://github.com/google/google-api-go-client). I haven't tried the other [Google Cloud Library for Go](https://github.com/GoogleCloudPlatform/google-cloud-go) since it didn't have the compute library I needed.

You can use the [`golang.org/x/oauth2/google`](https://godoc.org/golang.org/x/oauth2) library for authentication with this library. It can work with [service accounts](https://cloud.google.com/compute/docs/access/service-accounts) as well, which is what I am using at the moment.

### Using the GOOGLE_APPLICATION_CREDENTIALS environment variable

After you have created your service account, downloaded the JSON file, and saved it in some location, you can set the `GOOGLE_APPLICATION_CREDENTIALS` environment variable with the path of your service account JSON file.

{% highlight shell %}
# sample path is used
$ export GOOGLE_APPLICATION_CREDENTIALS=/tmp/service-acct.json
{% endhighlight %}

With that in place, the [Application Default Credentials Example](https://github.com/google/google-api-go-client#application-default-credentials-example) sample code should just work for you.

### Using the service account file directly to create the client

It's all fine and good if you only use one service account file all throughout the application but if you happen to need to use a specific JSON file per call, this section is for you.

{% gist 5241f3cb96b9dfb9a58e77a16be159fe %}
