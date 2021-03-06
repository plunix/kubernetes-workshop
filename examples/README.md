# Examples


## Useful Commands

Get kubectl version

    kubectl version

Get cluster info:

    kubectl cluster-info

Get pods

    kubectl get pods

Get all pods from all namespaces

    kubectl get pods --all-namespaces

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
    kubectl scale rc ping-update-initial --replicas=4
    kubectl rolling-update ping-update-initial --update-period=10s -f ping-rc-workshop.yaml


Debugging

    kubectl get events

You can get the logs of your containers easily too. If your pod runs more than one container `kubectl logs POD_NAME CONTAINER`
    kubectl logs redis-XXXXX

There are ways of interacting directly with your containers. For example, you can `exec` a command in your container. Like when doing a `docker exec...`
    kubectl exec redis-XXXXX -- redis-cli get ping

Or you can do port forwarding between your host and your container

    kubectl port-forward redis-XXXXX 6380:6379


Checking how the DNS works:

    kubectl exec busybox -- nslookup kubernetes
    kubectl exec busybox -- nslookup kubernetes.default
    kubectl exec busybox -- nslookup kubernetes.default.svc.cluster.local

Running pods directly using kubectl

    # start the pod running nginx
    kubectl run --image=nginx nginx-app --port=80 --env="DOMAIN=cluster"
    # expose a port through with a service
    kubectl expose rc nginx-app --port=80 --name=nginx-http

Your first cattle

    kubectl run nginx --image=nginx:1.9.12 # Thanks Kelsey!
    kubectl expose deployment nginx --port=80 --type=LoadBalancer


Create a ConfigMap from a file

    kubectl create configmap nginx-ghost --from-file=configs/ghost.conf --namespace=ghost
