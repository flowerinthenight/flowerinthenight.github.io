---
layout: post
title: "A Simple Folder/File Watcher In Powershell"
location: "Japan"
categories: ["Code"]
comments: true
---

Pardon the syntax hightlighting here. I'm using the `<pre>` tags at the moment as the highlighter fails with the following code.

<pre>
Param($MonitorFolder, $SleepInSec)

if (!$MonitorFolder) {
    Write-Host "You need to set -MonitorFolder parameter."
    Return
}

$sleep = 1
if ($SleepInSec) {
    $sleep = $SleepInSec
}

Write-Host "Sleep value = $sleep"

# Set folder, files (subfolders y/n) to watch.
Write-Host "Current PID = $pid"
$watcher = New-Object System.IO.FileSystemWatcher
$watcher.Path = "$MonitorFolder"
$watcher.Filter = "*.*"
$watcher.IncludeSubdirectories = $false
$watcher.EnableRaisingEvents = $true

# Action after event.
$action = { $path = $Event.SourceEventArgs.FullPath
    $changeType = $Event.SourceEventArgs.ChangeType
    $logline = "$(Get-Date), $changeType, $path"
    Write-Host "[PID = $pid] $logline"
    global:AddJobItem
}

# Decide which events should be watched.
$created = Register-ObjectEvent $watcher "Created" -Action $action
$changed = Register-ObjectEvent $watcher "Changed" -Action $action
$deleted = Register-ObjectEvent $watcher "Deleted" -Action $action
$renamed = Register-ObjectEvent $watcher "Renamed" -Action $action

# Main loop.
# while ($true) { sleep $sleep }

$global:startAddJob = 8

Write-Host "Script Starting."

$concurrentTasks = 4 # How many tasks can run at once.
$waitTime = 500 # Duration in ms the script waits to check for job status changes.

# $jobs holds pertinent job information. This is a test script so these are
# just simple values to track script progress.
$global:jobs = @("1", "2", "3", "4", "5", "6", "7")
$jobIndex = 0 # Which job is up for running
$workItems = @{} # Items being worked on
$workComplete = $false # Is the script done with what it needs to do?

Function global:AddJobItem()
{
    Write-Host "AddJobItem entry."
    $global:startAddJob += 1
    Write-Host "startAddJob = $startAddJob"
    $global:jobs += $startAddJob.ToString()
}

$oneTime = $false

while (!$workComplete) {
    # Process any finished jobs.
    foreach ($key in @() + $workItems.Keys) {
        # Write-Host "Checking job $key."
        if ($workItems[$key].State -eq "Completed") {
            "[$pid] $key is done."
            $result = Receive-Job $workItems[$key]
            $workItems.Remove($key)
            "[$pid] Result: $result"
        }
    }
    
    # Start new jobs if there are open slots.
    while (($workItems.Count -lt $concurrentTasks) -and ($jobIndex -lt $global:jobs.Length)) {
        # These jobs don't do anything other than wait a variable amount of time
        # and print an output message.
        $workTime = Get-Random -Minimum 2000 -Maximum 10000
        $global:job = $global:jobs[$jobIndex]
        "[$pid] Starting job {0}." -f $global:job
        
        $workItems[$global:job] = Start-Job -ArgumentList $workTime, $global:job -ScriptBlock {
            Start-Sleep -Milliseconds $args[0];
            "[$pid] {0} processed." -f $args[1]
        }
        
        $jobIndex += 1
    }
    
    # If all jobs have been processed we are done.
    if ($jobIndex -eq $global:jobs.Length -and $workItems.Count -eq 0) {
        # $workComplete = $true
        if (!$oneTime) {
            Write-Host "Initial job list done."
            Write-Host "Waiting for more jobs..."
            $oneTime = $true
        }
    }
    
    # Wait between status checks
    Start-Sleep -Milliseconds $waitTime
    # Write-Host "Wait = $waitTime"
}

Write-Host "Script Finished."
Read-Host "Press any key to end"
</pre>
