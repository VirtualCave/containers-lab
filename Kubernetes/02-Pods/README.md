# Pods

In Kubernetes, the [_pods_](https://kubernetes.io/docs/concepts/workloads/pods/) are the mininmum workload type to deploy. It is a group of one or more containers that share the same context like storage or network resources. Each _pod_ is isolated from the other by different Linux namespaces and cgroups so the containers inside the same pod can communicate with each other by calling _localhost_, and this means that the ports for each container must be unique.

## Deploying a Pod

In this first example we will deploy an _nginx_ _pod_ by using the kubectl command.

```
$ kubectl run --generator=run-pod/v1 nginx --image=nginx --namespace=container-lab-ns

pod/nginx created

$ kubectl get pods -n container-lab-ns

NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          25s

$ kubectl delete pod nginx -n container-lab-ns

pod "nginx" deleted
```

Or like the rest of Kubernetes objects we can generate the definition and run it.

```
$ kubectl apply -f pod-definitions/first-nginx.yml

pod/nginx created

$ kubectl get pods -n container-lab-ns

NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          28s
```

## Consuming a Pod

In this case we can check if it is running properly by running the command _port-forward_ that generates a bridge between our local computer and that specific container.

```
$ kubectl port-forward nginx -n container-lab-ns 8080:80

Forwarding from 127.0.0.1:8080 -> 80
Forwarding from [::1]:8080 -> 80
```

After this, we can consume the application in _localhost_ from our browser.

![Nginx default page](./screenshots/nginx.png)