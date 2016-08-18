---
layout: post
title: "My commonly used commands in GIT"
location: "Japan"
categories: ["Code"]
comments: true
---

For personal reference:

### Delete last commit

{% highlight shell %}
git reset --hard HEAD~1
{% endhighlight %}

### Delete local branch

{% highlight shell %}
git branch -d <branch-name>
{% endhighlight %}

or to force delete

{% highlight shell %}
git branch -D <branch-name>
{% endhighlight %}

### Delete branch from remote repository

{% highlight shell %}
git push origin --delete <remote-branch-name>
{% endhighlight %}

### Search for the merge commit from a specific commit

{% highlight shell %}
git log <SHA>..master --ancestry-path --merges
{% endhighlight %}

### Search for a commit message

{% highlight shell %}
git log | grep <pattern>
{% endhighlight %}

### List commits on range line of codes for one file

{% highlight shell %}
git blame -L<line#>,+<offset> -- <filename>
{% endhighlight %}

For example, three lines starting from line 257 of main.cpp

{% highlight shell %}
git blame -L257,+3 -- main.cpp
{% endhighlight %}

### History of a line (or lines) in a file

{% highlight shell %}
git log --topo-order --graph -u -L <line-start>,<line-end>:<file>
{% endhighlight %}

For example, history of line 155 of main.cpp

{% highlight shell %}
git log --topo-order --graph -u -L 155,155:main.cpp
{% endhighlight %}

### Compare (diff) a file from the current branch to another branch

{% highlight shell %}
git diff ..<target-branch> <path-to-file>
{% endhighlight %}

Or if `difftool` is configured

{% highlight shell %}
git difftool ..<target-branch> <path-to-file>
{% endhighlight %}

### Custom format for log

Add to global `.gitconfig` using `git config --global alias.logp "..."`

{% highlight shell %}
git log --pretty=format:'%Cred%h %C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)[%an]%Creset'
{% endhighlight %}
