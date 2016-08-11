---
layout: post
title: "A Simple Powershell Function To Import An Environment"
location: "Japan"
categories: ["Code"]
comments: true
---

A couple of days ago, I was working on a powershell-based script for mstests automation and I needed to call `vsdevcmd.bat` from Visual Studios tools folder.

{% highlight powershell %}
function Invoke-Environment([Parameter(Mandatory=1)][string]$Command, [switch]$Output, [switch]$Force)
{
    $stream = if ($Output) { ($temp = [IO.Path]::GetTempFileName()) } else { 'nul' }
    $operator = if ($Force) {'&'} else {'&&'}
    
    foreach($_ in cmd /c " $Command > `"$stream`" 2>&1 $operator SET")
    {
        if ($_ -match '^([^=]+)=(.*)')
        {
            [System.Environment]::SetEnvironmentVariable($matches[1], $matches[2])
        }
    }
    
    if ($Output)
    {
        Get-Content -LiteralPath $temp
        Remove-Item -LiteralPath $temp
    }
}
{% endhighlight %}

To use the function:

{% highlight powershell %}
Invoke-Environment '"C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools\VsDevCmd.bat"'
{% endhighlight %}
