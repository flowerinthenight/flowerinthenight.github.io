---
layout: page
title: About
permalink: /about/
---

{% include image.html url="../images/photo.jpg" caption="" width="300px" max_width="300px" align="right" %}

Hi, my name is Chew and welcome to my blog. That's me on the right, by the way. At the moment, I work as Head of Engineering at a startup called [Mobingi](https://mobingi.com/). I live in Japan with my wife (also in the picture). I love [reading](http://flowerinthenight.com/bookshelf/), especially [high fantasy](https://en.wikipedia.org/wiki/High_fantasy) with very interesting magic system. I also like music. I play a couple of instruments (bass, guitar, piano, and drums) although I'm not very good at any of them.

Also, why Flowerinthenight? Good question. If you are thinking about Flowerinthenight, the princess from Diana Wynne Jones' [Castle In The Air](https://en.wikipedia.org/wiki/Castle_in_the_Air_(novel)), then you are right. Congratulations! Anyway, it goes without saying that she is one of my favorite book characters of all time. Seriously, I can't think of any other princess with a name as fantastic as hers.

## Work history

* Head of Engineering, 2017-present &#124; [Mobingi, Japan](https://mobingi.com)
  * Acting CTO, overall architecture design, engineering management, recruitment
  * Go (golang), Microservices, DevOps, Docker, Kubernetes
  * Multicloud (AWS, GCP, Azure, AlibabaCloud/SBCloud)
* Senior Software Engineer, 2016-2017 &#124; [TeraRecon, Inc.](http://www.terarecon.com/)
  * Image processing, 2D/3D rendering (C#, C, C++, DICOM)
  * Microservices (Go, .NET Core, Service Fabric)
  * Front-end (Angular, JavaScript, TypeScript)
* Software Engineer, 2008-2016 &#124; [IBM/Lenovo](https://en.wikipedia.org/wiki/Lenovo#IBM)
  * Device driver development (WDM, KMDF, UMDF, Linux)
  * BIOS development (C, x86 ASM)
  * Video, camera, audio related development (DirectShow, Media Foundation, OpenCV, DirectX)
  * Windows development (Win32, MFC, COM, .NET, UWP)
  * Android development (framework level, JNI, C++)
  * Embedded systems
* Others (mostly C/C++)...

## Spoken languages
* English - proficient
* Japanese - conversational

## Education

BS in Computer Engineering &#124; 2000-2005

## Contact

<div>
{% if site.email_address %}
<a href="mailto: {{ site.email_address }}">
    <span class="fa-stack fa-lg">
        <i class="fa fa-circle fa-stack-2x"></i>
        <i class="fa fa-envelope fa-stack-1x fa-inverse"></i>
    </span>
</a>
{% endif %}

{% if site.twitter_username %}
<a href="https://twitter.com/{{ site.twitter_username }}">
    <span class="fa-stack fa-lg">
        <i class="fa fa-circle fa-stack-2x"></i>
        <i class="fa fa-twitter fa-stack-1x fa-inverse"></i>
    </span>
</a>
{% endif %}

{% if site.github_username %}
<a href="https://github.com/{{ site.github_username }}">
    <span class="fa-stack fa-lg">
        <i class="fa fa-circle fa-stack-2x"></i>
        <i class="fa fa-github fa-stack-1x fa-inverse"></i>
    </span>
</a>
{% endif %}
</div>
