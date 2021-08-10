# Kubernetes

<blockquote>
> Kubernetes originates from Greek, meaning helmsman or pilot
>  Google open-sourced the Kubernetes project in 2014.
> Open-source platform
> manager tons of containers and services
> PaaS (Platform as a Service) system

# What purpose does this serve 

In a production environment, you need to manage the containers that run the applications and ensure that there is no downtime. For example, if a container goes down, another container needs to start. Wouldn't it be easier if this behavior was handled by a system?

That's how Kubernetes comes to the rescue! Kubernetes provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, and more. For example, Kubernetes can easily manage a canary deployment for your system.

## Kube - API SERVER

The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.<br/>

The main implementation of a Kubernetes API server is kube-apiserver. kube-apiserver is designed to scale horizontally—that is, it scales by deploying more instances. You can run several instances of kube-apiserver and balance traffic between those instances.

## Kubectl

> The kubectl command line tool. sysadmin use this tool.
> This tool lets sysadmin control Kubernetes clusters.
> use kubectl to deploy applications, inspect and manage cluster resources, and view logs.
> `kubectl [command] [TYPE] [NAME] [flags]`
> command `create, get, describe, delete`
> TYPE: Specifies the resource type. Resource types are case-insensitive and you can specify the singular, plural, or abbreviated form
> `kubectl get pod pod1` 
> flags: Specifies optional flags. For example, you can use the -s or --server flags to specify the address and port of the Kubernetes API server.<br/>

## Wokers
When deploy Kubernetes, you get a cluster.
Kubernetes cluster consists of a set of worker machines, **called nodes**. <br>
> node run containerized application
> Every cluster has at least one worker node.
> The worker node(s) host the Pods 
> Pods are the components of the application workload.
> The control plane manages the worker nodes and the Pods in the cluster.


## PODS

Pods are the smallest, most basic deployable objects in Kubernetes. A Pod represents a single instance of a running process in your cluster.<br/>

Pods contain one or more containers, such as Docker containers. When a Pod runs multiple containers, the containers are managed as a single entity and share the Pod's resources. Generally, running multiple containers in a single Pod is an advanced use case.<br/>

1. Network: Pods are automatically assigned unique IP addresses. Pod containers share the same network namespace, including IP address and network ports. Containers in a Pod communicate with each other inside the Pod on localhost.<br/>

2. Storage: Pods can specify a set of shared storage volumes that can be shared among the containers.<br/>

**Pods run on nodes in your cluster**. Once created, a Pod remains on its node until its process is complete, the Pod is deleted, the Pod is evicted from the node due to lack of resources, or the node fails. If a node fails, Pods on the node are automatically scheduled for deletion.<br/>

## Nodes

A node may be a virtual or physical machine, depending on the cluster. Each node is managed by the control plane and contains the services necessary to run Pods.<br/>

The components on a node include the kubelet, a container runtime, and the kube-proxy.<br/>

> A Pod always runs on a Node.
> Every Kubernetes Node runs at least:

> **Kubelet, a process responsible for communication between the Kubernetes control plane and the Node;** it manages the Pods and the containers running on a machine.

> A container runtime (like Docker) responsible for pulling the container image from a registry, unpacking the container, and running the application.



[<img src="https://d33wubrfki0l68.cloudfront.net/5cb72d407cbe2755e581b6de757e0d81760d5b86/a9df9/docs/tutorials/kubernetes-basics/public/images/module_03_nodes.svg">](NODE)

## etcd storage

> It's a database
> use key-value method
> etcd is a consistent and highly-available key value store.
> it store all cluster data.

## Scheduler

The Kubernetes scheduler is a control plane process which assigns Pods to Nodes. The scheduler determines which Nodes are valid placements for each Pod in the scheduling queue according to constraints and available resources. <br>
A scheduler watches for newly created Pods that have no Node assigned. For every Pod that the scheduler discovers, the scheduler becomes responsible for finding the best Node for that Pod to run on. 

Scheduler ask pods where and which specific server the container needs to deployed or execute. 


</blockquote>