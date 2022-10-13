<p align="justify">
<strong>

# Getting Started with Kubernetes - <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=Kubernetes&logoColor=white">

![](https://github.com/amandewatnitrr/kubernetes-tutorial/blob/master/imgs/kubernetes-gcp.gif)

- Kubernetes, also known as `K8s`, is an open-source system built by Google based on there experience running containers in production for automating deployment, scaling, and management of containerized applications.
- It is now an Open-Source Project and is arguably one of the best and most popular Container Orchestration technologies out there.
- To understand Kubernetes, we must understand 2 things (You can find info on this in Docker Tutorial):
  - Container
  - Orchestration

<img align="right" width="10%" height="10%" src="https://github.com/amandewatnitrr/kubernetes-tutorial/blob/master/imgs/k8s.svg">

- Kubernetes is just a container orchestration technology. There are multiple such technologies available today. Docker has it's own tool called Docker Swarm, Kubernetes from Google and MESOS from Apache. While Docker swarm is really easy to setup and get started, it lacks some of the advanced features required for complex applications. MESOS on the other hand si quite difficult to setup and get started but supports many advanced features.
- Kubernetes arguably the most popular of all , is a bit difficult to setup and get started but provides a lot of options to customize deployments and supports deployment of complex architectures.
- It is now supported on all public cloud service providers like GCP, Azure and AWS. It is also one of the top most ranked projects on Github.
- There are various advantages of container orchestration:
  - The application is now highly available as hardware failures do not bring our application down because we have multiple instances of our application running on different nodes.
  - The user traffic is load balanced across various containers. When demand increases, deploy more instances of the application seamlessly and within a matter of seconds, and we have the ability to do that at a service level when we run out of hardware resources, scale the number of underlying hosts up or down without having to take down the application and do all of these easily with a set of declarative object configuration files.

</strong>
</p>