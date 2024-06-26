---
layout: post
title: "Automate Spanner backup using Kubernetes CronJob"
location: "Japan"
tags: [spanner, gcp, k8s, cronjob, backup]
---

As of this writing, GCP doesn't have an option to create [Spanner](https://cloud.google.com/spanner/) backups automatically. This could be available when you're reading this in the future. At the moment, however, if you're using Kubernetes, you can utilize [CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/) to do a scheduled backup.

Here's a sample CronJob deployment that uses `gcloud` to create the backups. First, you need to create a service account that has permissions to create Spanner backups. Once you have downloaded the JSON file for the service account, store it as a Kubernetes [Secret](https://kubernetes.io/docs/concepts/configuration/secret/).

{% highlight shell %}
$ kubectl create secret generic spannerbackup-keyfile --from-file svcacct.json
{% endhighlight %}

Make sure to update some of the information below as required, such as, name of the backup, instance name, database name, expiration date, etc. The example below uses the backup name `autobackup-yyyymmddthhmmssutc` format with a 3-day backup expiration.

{% highlight yaml %}
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: spannerbackup
  spec:
    concurrencyPolicy: Forbid
    # Run every day @ 2:30am JST (below is UTC)
    schedule: "30 17 * * *"
    jobTemplate:
      spec:
        template:
          spec:
            containers:
            - name: spannerbackup
              image: google/cloud-sdk:307.0.0-slim
              command: ["/bin/bash"]
              args: ["-c", "NAME=autobackup-$(date +%Y%m%dT%H%M%S%Z | awk '{print tolower($0)}'); EXP=$(date -u -d '+3 day' +%FT%TZ); gcloud auth activate-service-account --key-file $GOOGLE_APPLICATION_CREDENTIALS && gcloud spanner backups create $NAME --instance=<instancename> --database=<dbname> --expiration-date=$EXP --async"]
              env:
              - name: GET_HOSTS_FROM
                value: dns
              - name: GOOGLE_APPLICATION_CREDENTIALS
                value: /etc/spannerbackup/svcacct.json
              volumeMounts:
              - name: keyfile
                mountPath: "/etc/spannerbackup"
                readOnly: true
            restartPolicy: OnFailure
            volumes:
            - name: keyfile
              secret:
                secretName: spannerbackup-keyfile
{% endhighlight %}

Using backtick:

```yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: spannerbackup
  spec:
    concurrencyPolicy: Forbid
    # Run every day @ 2:30am JST (below is UTC)
    schedule: "30 17 * * *"
    jobTemplate:
      spec:
        template:
          spec:
            containers:
            - name: spannerbackup
              image: google/cloud-sdk:307.0.0-slim
              command: ["/bin/bash"]
              env:
              - name: GET_HOSTS_FROM
                value: dns
              - name: GOOGLE_APPLICATION_CREDENTIALS
                value: /etc/spannerbackup/svcacct.json
              volumeMounts:
              - name: keyfile
                mountPath: "/etc/spannerbackup"
                readOnly: true
            restartPolicy: OnFailure
            volumes:
            - name: keyfile
              secret:
                secretName: spannerbackup-keyfile
```

Finally, deploy to k8s.

{% highlight shell %}
# Assuming above file is saved as `backup.yaml`
$ kubectl create -f backup.yaml
{% endhighlight %}

