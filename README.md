# Week-7-Notes

MSA vs SOA: https://docs.google.com/presentation/d/1a6w8bIbKZ50N477NIIIoiXtCwavRG5RNO4DhNVfPwRs/edit#slide=id.g7e69f153f1_0_11
Karma and Jasmine doc (wont be on QC monday) https://docs.google.com/document/d/19UU3q0FowQ9ncfzK3kwKbvjmxQoFzt6F-ZjVi-XCaFQ/edit

# KUBERNETES & CONTAINER ORCHESTRATION
## What is Kubernetes?
Kubernetes is an open source container orchestration software that automatically creates, monitors, manages and scales workloads for you.

## What is Container Orchestration?
It is a way of automating the managing and scheduling of work for individual containers in conjunction with others in a container environment.

This allows us to run containers packed in large scales within a given environment.

## Basic Kubernetes Objects
Pod
Service
Volume
Namespace

### Pod
Pods are the most basic unit in a Kubernetes system and they contain at least one or more containers.
A Pod provides a wrapper around a container(s) to provide the abstraction that Kubernetes needs to scale out or know how to use the set of containers.
This allows us to make assumptions about the pod and then adapt the pod to the container.
Network resources are connected to each Pod.
The containers in a Pod share resources like secondary storage, CPU, and RAM.
The Pod enables you to deploy related containers side-by-side that need to be in the same environment in order to run proficiently.
A Pod also provides a way for taxonomy.  That is, it allows you to label each container within or name the Pod itself.

***
#### NOTE: Basic overview of Nodes and Clusters and their relation to Pods
Node - The physical machine (VMs, Physical Server, etc.) that runs your applications and cloud workflows from the Pods it contains.
Cluster - A set of multiple nodes collectively pursuing a commmon goal.

A Node contains 1 or more Pods
A Cluster contains 1 or more Nodes
A Master can be attached to multiple Clusters in order to orchestrate the running of containers and uses controllers for efficiency.
***

### Service
A Service is an abstraction which defines a logical set of pods and a policy by which to access those pods.
A Service does this through port exposure, which is an exposure of anything from Pods to Replica Sets or Controllers on a port by way of the Kube Proxy to an endpoint accessible to users.
Anytime you map an external port to an internal port in a load balance scenario, that is a Kubernetes Service.
A Service enables loose coupling between dependent Pods and is defined, like all Kubernetes objects, by a YAML or JSON.

#### Exposing a Service
Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods and can load balance across them.
This allows Pods to communicate across a network for better orchestration between dependent containers.
Although each Pod has a unique IP address, those IPs are not exposed outside the cluster without a Service.
Services allow your applications to receive traffic.
Services can be exposed in different ways by specifying a type in the ServiceSpec.

ServiceSpec Types:
ClusterIP
NodePort
LoadBalancer
ExternalName

#### Kube Proxy
The Kube Proxy determines which Pod (thus, container) will receive the incoming request.
The Kube Proxy does port forwarding from the external to internal port running on the Pod.
From here, you can do reverse proxies and load balancing.

### Volume
There are two problems that exist when dealing with data inside containers:
1.  The container always starts with a clean state, meaning when a container crashes, kubelet will restart it and file loss occurs.
2.  When running containers together in a Pod, it is often necessary to share files between those containers.

The Kubernetes Volume abstraction solves both of these problems by preserving data across container restarts.
A Volume is essentially a directory accessible to all containers running in a Pod.

### Namespace
Kubernetes supports multiple virtual Clusters backed by the same physical Cluster.
These virtual Clusters are called Kubernetes Namespaces.
Kubernetes Namespaces are a way to divide Cluster resources between multiple users (via resource quota).
In future versions of Kubernetes, objects in the same Namespace will have the same access control policies by default.

## Kubernetes Architecture
In a Kubernetes Architecture, Clusters of Nodes are tied to Master Nodes.
A Cluster needs 1 or more Masters to run.  This is because the Kubernetes Masters act as the control unit for clusters.
You'd typically have at least 3 Masters and 2 or more Nodes:
* If one Master Node fails the other picks up the weight so you don't lose the Cluster
* 2 Masters may compete on failure, so third is there to make sure the work still gets done.
* If one Node fails, you can shift the work to another.






