<p align="justify">
<strong>

# Replication Controllers and Replica Set - <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=Kubernetes&logoColor=white">

<img src="https://github.com/amandewatnitrr/kubernetes-tutorial/blob/master/imgs/full-stack-development5.gif">

- Controllers are the brain behind Kubernetes.
- They are the processes that monitor Kubernetes Objects and respond accordingly.

## What is `Replica`? And Why do we need a `Replication Controller`?

- Let's suppose our previous scenario where we had a Single POD running our application. What if for some reason our application crashes and the part fails? Users will no longer be able to access our application. To prevent users from losing access to our application, we would like to have more than 1 instance or POD running at the same time. That way if one fails, we still have our application running on the other one.

- The Replication Controller helps us run multiple instances of a Single POD in Kubernetes Cluster, thus providing high availability. So does that mean we can't use a Replication Controller if we plan to have a Single POD?
  - No, even if we have a single POD, The Replication Controller can help by bringing up a new POD when the existing one fails. Thus the Replication Controller ensures that the specified number of PODs are running at all times, even if it's just 1 or 100.
  - Another reason we need replication controller is to create multiple parts to share the load across them. For example, in a simple scenario where we have a single POD serving a set of users. When the number of users increase, we deploy additional POD to balance the load across 2 PODs.
  - If the demand further increases and if we were to run out of resources on first node, we could deploy additional PODs across the other nodes in the cluster. As we can see the Replication Controller spans across multiple nodes in the cluster. It helps us balance the load across multiple parts on different nodes as well as scale our application when the demand increases.

- It's important to note that there are 2 similar terms:
  - Replication Controller
  - Replica Set

  - Both have the same purpose, but they are not the same.
  - Replication Controller is the older technology that is being replaced by Replica Set.
  - Replica Set is the new recommended way to setup replication.
  - However, whatever we discussed till now in this article remain applicable to both these technologies.
  - There are minor differences in the way each work.

### Creating `Replication Controller`

- rc-definition.yml

    ```YAML

        apiVersion: v1
        kind: ReplicationController
        metadata:
            name: myapp-rc
            labels:
                app: myapp
                type: front-end

        spec:
            template:
                metadata:
                    name: my-app-pod
                    labels: 
                        app: myapp
                        type: frontend

                spec:
                    containers:
                      - name: nginx-container
                        image: nginx

    ```

- As with any other kubernetes file we have 4 sections. As we are creating a Replication Controller, it is supported in `apiVersion` `v1`. The `kind` is `ReplicationController`. Under metadata, we will add the name and we will also add a few labels => app and type and assign value to them.

- The next is the most crucial part of the definition file that is the specification.
- For any Kubernetes definition file, the spec section defines what's inside the object we are creating. In this case, we know that the replication controller creates multiple instances of a POD. But what POD?
- We create a template section under spec to provide a POD template to be used by the replication controller to create replicas.
- Now how do we define the POD template? Remember we created a POD definition file in the previous exercise. We can reuse the contents of the file to populate the template section.
- Move all the contents od the POD definition file into the template section of the Replication Controller except for the frist few lines which are apiVersion an kind.
- Remember whatever we move must be under the template section, meaning they should be properly intended to the right and have more spaces before them than the template line itself. They should be children of the template section.

- Looking at our file now, we now have 2 metadata sections. One is for the replication controller and another for the POD.

</strong>
</p>
