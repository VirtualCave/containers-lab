# Namespaces

A namespace in Kubernetes is a logical group of resources that allows to separate the usage of resources and privileges for the users that manages the cluster.

All the Kubernetes clusters starts with the following initial _namespaces_:

  - Default
  - Kube-system
  - Kube-public
  - Kube-node-lease

We can create our own namespaces to manage our resources by running a command.

```
$ kubectl create namespace container-lab-ns

namespace/container-lab-ns created

$ kubectl get namespaces

NAME                 STATUS   AGE
container-lab-ns     Active   22s
default              Active   121m
kube-node-lease      Active   121m
kube-public          Active   121m
kube-system          Active   121m
local-path-storage   Active   121m

$ kubectl get pods -n container-lab-ns

No resources found in container-lab-ns namespace.

$ kubectl delete namespace container-lab-ns

namespace "container-lab-ns" deleted

```

Or we can have a file with the namespace definition.

```
$ kubectl apply -f first-namespace/first-namespace.yml

namespace/container-lab-ns created

$ kubectl get namespaces

NAME                 STATUS   AGE
container-lab-ns     Active   27s
default              Active   128m
kube-node-lease      Active   129m
kube-public          Active   129m
kube-system          Active   129m
local-path-storage   Active   128m
```

