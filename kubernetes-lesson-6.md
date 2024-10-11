# Getting started with Helm

![](./imgs/hq720.jpg)

>[!IMPORTANT]
>`Helm` is a `package manager for Kubernetes` that allows you to define, install, and manage applications on your Kubernetes cluster. Helm packages are called charts, and they contain all the Kubernetes resources needed to run an application, such as deployments, services, and ingress rules.

- So, it's a convinient way for packaging collections of Kubernetes yaml files, and distributing them in public and private repositories/regisitries.

- Let's say we have deployed our application in kubernetes cluster, and you want to deploy Elastic Stack additionally in your cluster that our application will use to collect it's logs.

  In order to deploy Elastic Stack, in your kubernetes cluster, we will need a couple of Kubernetes Components, we will need a statefulset which is meant for stateful applications, a ConfigMap for external configuration, A Secret for credential storage and K8s user with respective permissions and also create couple of services.

  Now, if we were to create all these files manually by searching for each one of them or doing own brain work would be a tedious task.

  So, it makes complete sense that someone created all these yaml files packaged them and published them over onto a public repository/regisitry for people to use.

  And these bundle of yaml files are called `Charts` in Helm or `Helm Charts`.

>[!NOTE]
>A Helm chart is a package that contains all the resources required to deploy an application to a Kubernetes cluster.

- Commonly used deployment like Database applications, elasticsearch or MongoDB, MySQL or monitoring applications like Prometheus, Grafana that have kind of complex setup all have charts available in some Helm Repository.

- Using the command:

  ```bash
  helm install <chart-name> <release-name>
  ```

  we can reuse the configuration that someone else has already made without additional effort and deploy the application in our cluster.

  We can look for the Charts using the command:

  ```bash
  helm search repo <chart-name>
  ```

>[!NOTE]
>Another functionality of `Helm` is it's also a templating engine.

- Imagine you have an application made up of multiple microservices, and I am deploying all of them in my k8s cluster, and deployment and services of each of those microservices are pretty much the same with only difference that the application name and the version name are different or docker image name and version tags are different.

  So, without helm you will write seprate yaml files, configuration files for each of those microservices, so you would have multiple deployment service files, where each has it's own application name and verison defined.

  Using Helm, what we can do is we can define a common blueprint for all those services, the values that are dynamic or are going to be changed replaced by placeholders. And, that would be a template file.

  And, would look something like this:

  ```yaml
  appVersion: v1
  kind: Pod
  metadata:
    name: {{ .Values.appName }}
  spec:
    containers:
      - name: {{ .Values.appName }}
        image: {{ .Values.image }}
        ports:
          - containerPort: 80
  ```

  Here, one can clearly say that instead of values in some places, we have the syntax which means that we are taking a value from external configuration.

  And, if you see carefully there's something called `Values` which is a special object in Helm that allows you to pass values to the template file.

  These Values are defined in `values.yaml` file.

  `Values.yaml`

  ```yaml
  name: my-app
  container: my-app-image:v1
    name: my-app
    image: my-app-image:v1
    port: 80
  ```

  `.Values` is a special object that's been created based on the values that are supplied via `values.yaml` file or via CLI using `--set` flag.

  So, which ever way you define them these values are put together in `.Values` object that you can than use in those template files to get the values out.

- So, now instead of having YAML files for each microservice or application, we just have one and we can just simply replace those values. It is practically beneficial when you are using CI/CD pipelines.

  Cause there in the build files, we can replace the values in those template yaml files on the fly and deploy them in the cluster.

- Another, use case for Helm comes into picture when we deploy the same application across different environments from k8s cluster.