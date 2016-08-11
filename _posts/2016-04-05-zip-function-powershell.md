---
layout: post
title: "A Simple Zip Function In Powershell"
location: "Japan"
categories: ["Code"]
comments: true
---

{% highlight powershell %}
function ZipFiles($ZipFileName, $SourceDir)
{
    Add-Type -Assembly System.IO.Compression.FileSystem
    $compressionLevel = [System.IO.Compression.CompressionLevel]::Optimal
    [System.IO.Compression.ZipFile]::CreateFromDirectory($SourceDir, $ZipFileName, $compressionLevel, $false)
}
{% endhighlight %}

To use the function:

{% highlight powershell %}
ZipFiles -ZipFileName test.zip -SourceDir .\folder\to\zip
{% endhighlight %}
