---
layout: post
title: "A Simple Signal Handler In C/C++ (Linux)"
location: "Japan"
categories: ["Code"]
comments: true
---

Personal reference:

{% highlight cpp %}
#include <iostream>
#include <signal.h>
#include <unistd.h>
#include <sys/file.h>

// signal handler
void signal_handler(int s)
{
    std::cout << "Caught signal: " << s << std::endl;
    exit(1);
}

// entry
int main(int argc, char* argv[])
{
    // setup signal handler
    struct sigaction sigIntHandler;

    sigIntHandler.sa_handler = signal_handler;
    sigemptyset(&sigIntHandler.sa_mask);
    sigIntHandler.sa_flags = 0;
    sigaction(SIGINT, &sigIntHandler, NULL);

    std::cout << "Press Ctrl+C to exit." << std::endl;

    for (;;) {
        sleep(1);
    }

    return 0;
}
{% endhighlight %}
