# Local Installation

For this Lab, the first thing to get is a Kubernetes cluster, so in case you have not one available yet, follow this instructions to run your own local cluster. Here we will explain how to install [KinD](https://kind.sigs.k8s.io/) and after that, how to test if it is running properly.

## KinD installation

We will explain the procedure for Linux environments, but if you need other one, follow the instructions in the [official documentation page](https://kind.sigs.k8s.io/docs/user/quick-start/#installation). 

First we need to download the binary and move it somewhere the $PATH will load it. 

```
$ curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64
$ chmod +x ./kind
$ mv ./kind /usr/bin/kind
```
To check if the installation was correct we need to reload the $PATH opening a new terminal.

```
$ kind -h
kind creates and manages local Kubernetes clusters using Docker container 'nodes'

Usage:
  kind [command]

Available Commands:
  build       Build one of [node-image]
  completion  Output shell completion code for the specified shell (bash, zsh or fish)
  create      Creates one of [cluster]
  delete      Deletes one of [cluster]
  export      Exports one of [kubeconfig, logs]
  get         Gets one of [clusters, nodes, kubeconfig]
  help        Help about any command
  load        Loads images into nodes
  version     Prints the kind CLI version

Flags:
  -h, --help              help for kind
      --loglevel string   DEPRECATED: see -v instead
  -q, --quiet             silence all stderr output
  -v, --verbosity int32   info log verbosity
      --version           version for kind

Use "kind [command] --help" for more information about a command.
```

Now it is time to create our cluster.

```
$ kind create cluster --help
Creates a local Kubernetes cluster using Docker container 'nodes'

Usage:
  kind create cluster [flags]

Flags:
      --config string       path to a kind config file
  -h, --help                help for cluster
      --image string        node docker image to use for booting the cluster
      --kubeconfig string   sets kubeconfig path instead of $KUBECONFIG or $HOME/.kube/config
      --name string         cluster name, overrides KIND_CLUSTER_NAME, config (default kind)
      --retain              retain nodes for debugging when cluster creation fails
      --wait duration       wait for control plane node to be ready (default 0s)

Global Flags:
      --loglevel string   DEPRECATED: see -v instead
  -q, --quiet             silence all stderr output
  -v, --verbosity int32   info log verbosity


$ kind create cluster --name container-lab-cluster
Creating cluster "container-lab-cluster" ...
 ✓ Ensuring node image (kindest/node:v1.21.1) 🖼 
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-container-lab-cluster"
You can now use your cluster with:

kubectl cluster-info --context kind-container-lab-cluster

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/


$ kind get clusters
container-lab-cluster
```

The cluster is created, as KinD runs over Docker Engine, we can check what has deployed for us.

```
$ docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS          PORTS                       NAMES
255a3808e1e7   kindest/node:v1.21.1   "/usr/local/bin/entr…"   11 minutes ago   Up 11 minutes   127.0.0.1:38817->6443/tcp   container-lab-cluster-control-plane
```

## Kubectl installation

Now, let's configure the access to our cluster. To operate the cluster we need Kubernetes CLI (kubectl) installed. We can do that following the official documentation for the different platforms. For linux you can run the following.

```
$ curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"

$ chmod +x ./kubectl

$ sudo mv ./kubectl /usr/local/bin/kubectl

$ kubectl version --client

Client Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.4", GitCommit:"8d8aa39598534325ad77120c120a22b3a990b5ea", GitTreeState:"clean", BuildDate:"2020-03-12T21:03:42Z", GoVersion:"go1.13.8", Compiler:"gc", Platform:"linux/amd64"}
```

We also need a KubeConfig file where will be stored the credentials for our user. By default, _kubectl_ (Kubernetes CLI) will use the ~/.kube/config file, but we can use a different file by exporting the environment variable $KUBECONFIG.

As the cluster we have deployed is new, we will get the kubeconfig file by using the KinD commands.

```
$ kind get kubeconfig --name container-lab-cluster > ~/.kube/container-lab-config

$ cat ~/.kube/container-lab-config

apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: SOME_LONG_STRING
    server: https://127.0.0.1:38817
  name: kind-container-lab-cluster
contexts:
- context:
    cluster: kind-container-lab-cluster
    user: kind-container-lab-cluster
  name: kind-container-lab-cluster
current-context: kind-container-lab-cluster
kind: Config
preferences: {}
users:
- name: kind-container-lab-cluster
  user:
    client-certificate-data: OTHER_SOME_LONG_STRING
    client-key-data: AND_OTHER_SOME_LONG_STRING

$ export KUBECONFIG=~/.kube/container-lab-config

$ kubectl get pods -A

NAMESPACE            NAME                                                          READY   STATUS    RESTARTS   AGE
kube-system          coredns-558bd4d5db-snhpp                                      1/1     Running   0          42m
kube-system          coredns-558bd4d5db-xx7k7                                      1/1     Running   0          42m
kube-system          etcd-container-lab-cluster-control-plane                      1/1     Running   0          42m
kube-system          kindnet-nvd5d                                                 1/1     Running   0          42m
kube-system          kube-apiserver-container-lab-cluster-control-plane            1/1     Running   0          42m
kube-system          kube-controller-manager-container-lab-cluster-control-plane   1/1     Running   0          42m
kube-system          kube-proxy-xbmcn                                              1/1     Running   0          42m
kube-system          kube-scheduler-container-lab-cluster-control-plane            1/1     Running   0          42m
local-path-storage   local-path-provisioner-547f784dff-k4nd9                       1/1     Running   0          42m
```
There are all the different elements that set our cluster like the Api Server, Controller, Kube-Proxy and the other elements.

## Section complete....

Now we have our cluster ready, we can continue with the lab by creating some [_namespaces_](../01-Namespaces/README.md).

