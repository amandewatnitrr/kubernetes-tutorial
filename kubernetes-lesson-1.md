<p align="justify">
<strong>

# Getting Started with Kubernetes - <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=Kubernetes&logoColor=white">

![](https://github.com/amandewatnitrr/kubernetes-tutorial/blob/master/imgs/kubernetes-gcp.gif)

- Kubernetes, also known as `K8s`, is an open-source system built by Google based on there experience running containers in production for automating deployment, scaling, and management of containerized applications.
- It is now an Open-Source Project and is arguably one of the best and most popular Container Orchestration technologies out there.
- To understand Kubernetes, we must understand 2 things (You can find info on this in Docker Tutorial):
  - Container
  - Orchestration

<img align="right" width="50%" height="50%" src="https://github.com/amandewatnitrr/kubernetes-tutorial/blob/master/imgs/k8s.svg">

- Kubernetes is just a container orchestration technology. There are multiple such technologies available today. Docker has it's own tool called Docker Swarm, Kubernetes from Google and MESOS from Apache. While Docker swarm is really easy to setup and get started, it lacks some of the advanced features required for complex applications. MESOS on the other hand si quite difficult to setup and get started but supports many advanced features.
- Kubernetes arguably the most popular of all , is a bit difficult to setup and get started but provides a lot of options to customize deployments and supports deployment of complex architectures.
- It is now supported on all public cloud service providers like GCP, Azure and AWS. It is also one of the top most ranked projects on Github.
- There are various advantages of container orchestration:
  - The application is now highly available as hardware failures do not bring our application down because we have multiple instances of our application running on different nodes.
  - The user traffic is load balanced across various containers. When demand increases, deploy more instances of the application seamlessly and within a matter of seconds, and we have the ability to do that at a service level when we run out of hardware resources, scale the number of underlying hosts up or down without having to take down the application and do all of these easily with a set of declarative object configuration files.

# Kubernetes Architecture

<img align="center" style="display: block;  margin-left: auto;  margin-right: auto;" src="https://github.com/amandewatnitrr/kubernetes-tutorial/blob/master/imgs/full-stack-development.gif"></img>

## Node

- A `Node` is a machine, physical or virtual on which Kubernetes is installed. A node is a worker machine and that is where container will be launched by Kubernetes.
- Previously, it was also known as `Minions`. Sometimes you might hear this term being used interchangeably.
- But what if the node on which our application is running fails?? Well Obviously our application goes down. So, you need to have more than one nodes.
- A Cluster is a set of nodes grouped together. This way even if one node fails, we have our application still accessible from other nodes.
- Moreover having multiple nodes helps in sharing loads as well.

## Master

- Now, we have the cluster but who is responsible for managing the cluster. Where is the information about members of cluster stored? How are the nodes monitored? When a node fails how do you move the workload of the field node to another worker node?
- That's where the master comes in.
- The `Master` is another node with Kubernetes installed on it and is configured as master. The master watches over the nodes in the cluster andd is responsible for actual orchestration of containers on the worker nodes.

## Components

- When we install kubernetes on a system, we are actually installing a number of components such as an
  - API Server
  - ETCD Service
  - Kubelet service
  - Container Runtime
  - Controllers
  - Schedulers
  
- API Server: 
  - The API Server acts as the Front-end of Kubernetes Service. 
  - The Users, Management Devices, CLI all talk to the API Server to interact with Kubernetes Cluster.

- ETCD Key-Value Store:
  - ETCD is a distributed reliable key-value store used by Kubernetes to store all data used to manage the cluster.
  - Think of this way when we have multiple nodes and multiple masters in our cluster, ETCD stores all that information on all the nodes in the cluster in a distributed manner.
  - It is responsible for implementing blocks within the cluster to ensure that there are no conflict b/w masters.

- Scheduler:
  - The Scheduler is responsible for distributing work or containers across multiple nodes.
  - It looks for newly created containers and assigns them to nodes.

- Controllers:
  - Controllers are the brain behind the orchestration
  - Responsible for noticing and responding when nodes, endpoints or containers goes down. They make the decisions to bring up new containers in such cases.

- Container Runtime:
  - Container Runtime is the underlying software that is used to run containers. 
  - In our cases this happens to be docker let's suppose it for now as there are other options as well.

- Kubelet
  - Kubelet is the agent that runs on each node in the cluster.
  - The agent is responsible for making sure that containers are running on the nodes as expected.

</strong>
</p>