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

<hr>

## Master vs Worker Nodes

- So, far we have seen 2 types of Servers:
  - Master
  - Worker
  - Set of Components
- They all together make Kubernetes.
- But how are these components distributed across different types of server?? In other words, how a server becomes master and the other become slave?
- The `Worker` Node or `Minion` as it is also known is where the containers are hosted.
- The `Worker` nodes have `Container Runtime`.
- For example, docker containers are needed to run docker container on a system, we need container runtime installed and that's where container runtime falls. In this case it happens to be docker. This doesn't have to be docker only. There are other container runtime alternatives available such as Rocket or Cryo. For this complete tutorial guide, we will suppose docker as our Container Runtime.
- The `Master` Server has the `KubeAPI Server` and that is what makes it a master.
- Similarly, the `Worker` nodes have the `Kubelet Agent` that is responsible for interacting with a master, to provide health information of the worker node and carry out action requested by Master on the worker nodes.
- All the information gathered are stored in a `key-value store` on the `master`. It is based on most popular ETCD Framework.
- The `Master` also has the `Scheduler` and the `Controller`.

## KubeCtl

- In parallel, let's not forget about one of the command line utilities Known as `Kube Command Line Tool` or `KubeCtl` or `Kube Control` as it is also called.
- The `KubeCtl` tool is used to deploy and manage applications on a Kubernetes Cluster.
- To get Cluster Information, to get status of other nodes in the cluster and to manage many other things.
- The `kubectl run` command is used to deploy an application on the cluster.
- The `kubectl cluster-info` command is used to view information about the cluster.
- The `kubectl get nodes` command is used to get list of all the nodes that are part of the cluster.

# Setting up Kubernetes

- There are multiple ways to setup Kubernetes. We can set it up ourselves locally on our laptops or virtual machines using solutions like :
  - minikube
  - microK8s
  - Kudeadm.
- The KubeAdmin tool is used to bootstrap and manage production grade kubernetes clusters.

- There are also hosted solutions available for Setting Up Kubernetes in cloud environment such as:
  - <img src="https://img.shields.io/badge/Google_Cloud-326CE5?style=plastic&logo=googlecloud&logoColor=white">
  - <img src="https://img.shields.io/badge/Amazon_Web_Service-232F3E?style=plastic&logo=googlecloud&logoColor=white">
  - <img src="https://img.shields.io/badge/Microsoft_Azure-0078D4?style=plastic&logo=MicrosoftAzure&logoColor=white">
  - <img src="https://img.shields.io/badge/IBM_Cloud-1261FE?style=plastic&logo=IBMCloud&logoColor=white">

## MiniKube

- Earlier we talked about different components of Kubernetes that make up master and worker node, such as the API Server, Key-Value Store, Controllers, Scheduler on the `Master` and the Container Runtime, KubeCtl Agent or Kubelet Service on the `Worker Node/Minion`.
- It takes a lot of time and effort to setup and install all of these various components systems individually by ourselves.
- MiniKube Bundles all of these different component into single image, providing us a pre-configured single node, kubernetes cluster, so we can get started in a matter of minutes.
- The Whole bundle is packaged into an ISO image and is available online for download.
- MiniKube provides an executable command line utility that automatically download the ISO and deploy it in a virtualization platform such as <img src="https://img.shields.io/badge/Oracle-F80000?style=plastic&logo=Oracle&logoColor=white">, <img src="https://img.shields.io/badge/Virtual_Box-183A61?style=plastic&logo=VirtualBox&logoColor=white"> and <img src="https://img.shields.io/badge/vmware-607078?style=plastic&logo=VMware&logoColor=white">.
- So, you must have a hypervisor installed on your system.
- For Windows, we can use VirtualBox or Hyper-V and for Linux, VirtualBox or KVM.
- And finally to interact with Kubernetes , you must have the KubeCtl Kubernetes command Line Tool also installed on your machine.

</strong>
</p>