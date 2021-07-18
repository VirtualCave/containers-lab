# Kubernetes (K8s)

Kubernetes is an open-source containers orchestrator developed originally by Google that was released in 2014. It allows to manage containerized workloads and services with a declarative configuration.

It offers multiple functionalities that helps in the management of the applications:
  - Service discovery
  - Load Balancing
  - Storage orchestration
  - Self Healing
  - Secret management
  - Automated deployments

Kubernetes have a lot of internal components that provides those functionalities:

  - Control Plane
    - Api Server: The Kubernetes Control Plane that provides APIs for the different applications. Clients must have connectivity from outside the cluster to operate.
    - Scheduler: Determines whether a cluster is healthy; and determines whether new containers should be deployed, and if so, where they should be placed.
    - Controller Manager: This service is controlls that all the different objects are in the state that they should. If the state not match, it takes actions to reach that correct state.
    - ETCD: It's a distributed open-source key/value store database that stores configurations and information about the state of the different services in the cluster.
  - Cluster Architecture
    - Workload Node: Those nodes in the cluster where the application pods will be running.
    - Kubelet: Runs in each workloads node and is in charge of communicate with the Control Plane if some action must be taken to reach a steady state of a node.
    - Kube-proxy: Network proxy that runs on each Workload Node and helps in the networking services. It is in charge of redirect traffic to the corresponding pod or service.

## Kind

One of the main problems that Kubernetes has is how hard is to configure all the different components of the cluster where all the containerized applications will run, like the ETC, the Api Server,... This means that for the developers it is very difficult to test their applications running en Kubernetes in local environments. To solve that there are some tools that helps to emulate K8s. 

In this Lab we will use [KinD](https://kind.sigs.k8s.io/) (Kubernetes in Docker) but you can use others like [MiniKube](https://minikube.sigs.k8s.io/docs/start/), [K3s](https://k3s.io/), [K3D](https://k3d.io/) or create a managed cluster in any public cloud privider you want ([EKS](https://aws.amazon.com/es/eks/), [GKE](https://cloud.google.com/kubernetes-engine), [AKS](https://azure.microsoft.com/es-es/services/kubernetes-service/)).
