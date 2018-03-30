---
layout: post
title: "Accessing pods in Kubernetes"
location: "Japan"
tags: [kubectl, Kubernetes]
---

When developing services that run on Kubernetes, at [Mobingi](https://mobingi.com), we generally use [Minikube](https://github.com/kubernetes/minikube) or [Kubernetes in Docker for Mac](https://blog.docker.com/2018/01/docker-mac-kubernetes/). We also have a cluster that runs on [GKE](https://cloud.google.com/kubernetes-engine/) that we use for development. In this post, I will share how we access some of the services that are running on our development cluster.

## Using kubectl port-forward

Using [kubectl port-forward](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/) is probably the cheapest and the most straightforward. For example, if I want to access a cluster service `svc1` through my localhost, I use `kubectl port-forward` like this:

{% highlight shell %}
$ kubectl get pod
NAME                            READY     STATUS    RESTARTS   AGE       IP           NODE
svc1-66dd787767-d6b22           2/2       Running   0          7d        ...          ...
svc1-66dd787767-ks92f           2/2       Running   0          7d        ...          ...
svc2-578786c554-rlw2w           2/2       Running   0          7d        ...          ...

# Connect to the first in the list (if multiple pods) of gcpd:
$ cat DigiCertCA.crt >> tls.crt
$ cp filename.key tls.key
$ kubectl create secret tls mytls --key tls.key --cert tls.crt
{% endhighlight %}

I was able to successfully use the secret in a GCE Ingress:

{% highlight ruby %}
apiVersion: extensions/v1beta1
kind: Ingress
...
spec:
  tls:
  - secretName: mytls
  backend:
    serviceName: myservice
    servicePort: 80
...
{% endhighlight %}

