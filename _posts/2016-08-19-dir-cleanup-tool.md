---
layout: post
title: "Simple directory cleanup tool for Windows (golang)"
location: "Japan"
categories: ["Code", "golang"]
comments: true
---

For personal reference:

{% highlight go %}
package main

import (
    "flag"
    "io/ioutil"
    "log"
    "os"
    "os/exec"
    "time"
)

func main() {
    pathPtr := flag.String("path", "", "The `DIRPATH` to clean up. Only sub-items are inspected.")
    beforePtr := flag.Int("sub", 30, "No. of `DAYS` ago. All items modified before that are deleted.")
    flag.Parse()

    if *pathPtr == "" {
        panic("No -path provided.")
    }

    files, err := ioutil.ReadDir(*pathPtr)
    if err != nil {
        panic(err)
    }

    now := time.Now()
    before := now.AddDate(0, 0, *beforePtr*-1)
    log.Println("All items modified before", before.Format(time.UnixDate), "will be deleted.")

    for _, f := range files {
        p := *pathPtr + "\\" + f.Name()
        mt, err := os.Stat(p)
        if err != nil {
            log.Println(err)
        } else {
            if mt.ModTime().Before(before) {
                log.Println("Deleting", p, "...")
                if mt.IsDir() {
                    c := exec.Command("cmd", "/C", "rmdir", "/s", "/q", p)
                    if err := c.Run(); err != nil {
                        log.Println(err)
                    }
                }
            }
        }
    }
}
{% endhighlight %}
