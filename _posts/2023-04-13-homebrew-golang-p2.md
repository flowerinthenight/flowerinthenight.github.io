---
layout: post
title: "Using Homebrew for distributing Go apps (part 2)"
location: "Japan"
tags: [homebrew, go, golang, goreleaser, homebrew, ruby]
---

For personal reference:

This is a followup on a [previous post](https://flowerinthenight.com/blog/2019/07/30/homebrew-golang) that is a bit more manual. This is a little bit easier.

#### a) Create your own Homebrew tap

Create a new GitHub public repository with a prefix `homebrew-`, i.e. `homebrew-tap`. This will host all the apps that you want to distribute via your tap. Users will install your apps using the following commands:

{% highlight shell %}
# No need to include the 'homebrew-' prefix
$ brew tap flowerinthenight/tap
$ brew install <toolname>

# Or one-liner
$ brew install flowerinthenight/tap/<toolname>
{% endhighlight %}

#### b) Let's use Github Actions to setup [goreleaser](https://github.com/goreleaser/goreleaser)

First, add a `.goreleaser.yml` config file to your Go repo. Here's an example:

<script src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2Fflowerinthenight%2Fkubepfm%2Fblob%2Fmaster%2F.goreleaser.yml&style=default&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on"></script>

The section of note here is the `brews:` part.

Here's an example of a GitHub Action config on how to setup [goreleaser](https://github.com/goreleaser/goreleaser) to do the release for our tags.

<script src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2Fflowerinthenight%2Fkubepfm%2Fblob%2Fmaster%2F.github%2Fworkflows%2Fmain.yml&style=default&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on"></script>

See the `name: Run goreleaser` section. You need to add a personal access token with `repo, workflow, write:packages` permissions to your repository's secrets. In this example, the name used is `GH_PAT` but you can use other names as well.

#### c) Do a tagged release

Tagged releases will do a deployment to your tap.

{% highlight shell %}
$ git tag v1.0.0
$ git push --tags
{% endhighlight %}

