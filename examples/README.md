# Examples


This repo contains a few examples of code, containers and kubernetes artifacts to help to understand the concepts behind kubernetes.

* [Ping](ping): a simple http endpoint. You can see the difference of names, labels and selectors, and how they work.
* [PingPodRedis](pingpodredis): a simple http endpoint that reads & writes to a Redis database. Both containers are in a Pod. State is not maintained.
* [Ping-redis](ping-redis):  a simple http endpoint that reads & writes to a Redis database. It runs on different Pods using an internal service. State is not maintained either.
*


## Useful Commands

Get cluster info:

    kubectl cluster-info

Get pods

    kubectl get pods

Get pods by label

    kubectl get pods -l env=production

Get services

    kubectl get services

Describe a service: handy when you want to get the public dns

    kubectl describe service pingredis

Scaling up & down

    kubectl scale --replicas=3 rc pingredis

Check your pods are created

    kubectl get pods

Delete one of them to see how a new one is created

    kubectl delete pod pingredis-XXXXX

Rolling Update

    kubectl create -f ping/k8s/ping-rc.yaml
    kubectl scale --replicas=3 rc pingrcname
    kubectl rolling-update pingrcname --update-period=10s -f ping/k8s/ping-rc-workshop.yaml


Debugging

    kubectl get events

You can get the logs of your containers easily too. If your pod runs more than one container `kubectl logs POD_NAME CONTAINER`
    kubectl logs redis-XXXXX

There are ways of interacting directly with your containers. For example, you can `exec` a command in your container. Like when doing a `docker exec...`
    kubectl exec redis-XXXXX -- redis-cli get ping

Or you can do port forwarding between your host and your container

    kubectl port-forward -p redis-XXXXX 6380:6379

