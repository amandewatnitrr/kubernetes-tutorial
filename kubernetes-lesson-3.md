<p align="justify">
<strong>

# Deployments - <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=Kubernetes&logoColor=white">

<img src="https://github.com/amandewatnitrr/kubernetes-tutorial/blob/master/imgs/tumblr_85b9b86937506df32e63831251a8fab5_2532cbc5_1280.gif">

- For now let us forget about PODs and Replica Sets and other Kubernetes Concept and discuss about how you might want to deploy  your application  in a production environment.
- Say, for example we have a web server that needs to be deployed in a production environment. We need not one but many such instances of the web server running for obvious reasons.
- Secondly, whenever newer versions of application builds become available on the docker registry , we would like to upgrade our docker instances seamlessly.
- However when we upgrade our instances we donot want to upgrade all of them at once as this might impact users accessing our applications so you might want to upgrade them one after the other and that kind of update is know as Rolling Updates.
- Suppose one of the upgrades we performed resulted in an unexpected error and you are asked to undo the recent change, you would like to be able to roll back the changes that were recently carried out.
- Finally, say for example you would like to make multiple changes to your environment such as upgrading the underlying web server versions as well as scaling our environment and also modifying the resource allocations etc.
- We donot want to apply each change immediately after the command is run, instead we would like to apply a pause to our environment, make the changes and then resumes so that all the changes are rolled out together. All of these capabilities are available with the Kubernetes deployments.
- Throughout this tutorial guide we discussed about PODs which deploy single instances of our application such as the web application in this case. Each container is encapsulated in PODs. Multiple such PODs are deployed using replication controllers or replica set and then comes deployment which is a Kubernetes Object that comes higher in the hierarchy, the deployment provides us with the capability to upgrade ht e underlying instances seamlessly using rolling updates, undo changes and pause and resume changes as required.

## Creating Deployment

-

  ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
        name: myapp-deployment
        labels:
            app: myapp
            type: front-end
    spec:
        template:
            metadata:
                name: myapp-pod
                labels:
                    app: myapp
                    type: front-end
            spec:
                containers:
                    - name: nginx-container
                      image: nginx
        replicas: 3
        selector:
            matchLabels:
                type: front-end

  ```

- As with the previous component, we first create the deployment definition file, the contents of the deployment definition file are exactly similar to the replica set definition file, except for the `kind` which is now set to be `Deployment`. The `apiVersion` is set to `apps/v1`. `metadata` which has names and labels and `spec` that has a `template`, `replicas` and `selector`.
- The `template` has a POD definition inside it. Once the file is ready run the `kubectl create -f deployment-definition.yml` command. Then run the `kubectl get deployment` command to see newly created deployment. The deployment automatically creates a replica set. If we run the `kubectl get replicaset` command we will be able to see a new replica set in the name of deployment. The Replica Set ultimately creates PODs. So, if we run the `kubectl get pods` command , we will be able to see POD name with the name of deployment and the replica set.
- So far there hasn't been much of a difference b/w replica set and the deployments except for the fact that deployment created a new Kubernetes object called deployments.

# Kubernetes Networking

- We will start with a single node Kubernetes Cluster. The node has an IP Address. Say it is one 192.160.8.1.2. in this case, this is the IP address we use to access the Kubernetes node, SSh into it etc..
- On a side note remember if we are using a minikube setup , then we are talking about the IP Address of the miniKube Virtual Machine inside your hypervisor.
- So, on the single node Kubernetes Cluster, we have created a single POD. As you know, a POD hosts a container, unlike in the Docker World where an IP address is always assigned to a docker container. In Kubernetes World IP Address is assigned to a POD. Each POD in the Kubernetes gets it's own internal IP Addresses. In our case, assume it to be in the range 10.244 series and the IP assigned to the POD is 10.244.0.2. So how its it getting this IP address??

</strong>
</p>
