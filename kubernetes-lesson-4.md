<p align="justify">
<strong>

# Microservices Application - <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=Kubernetes&logoColor=white">

<img src="https://github.com/amandewatnitrr/kubernetes-tutorial/blob/master/imgs/micro2.png">

<br>

- For this particular example and demonstration, we are going to use a simple application developed by Docker to demonstrate the various features available in running an application stack on docker. So let's first get familiarized with the application  because we will be working with the same application in different sections throughout the demonstration.

- This is a sample voting application which provides an interface for user to vote and another interface to show the results. The application consists of various components such as the voting app, which is a web application developed in python to provide user with an interface to choose b/w two options `A` and `B`. When we make a selection the vote is stored in Redis. For those who are new to Redis, Redis in this case serves as a database in memory. This vote is than processed by the worker, which is an application written in `.NET`. The Worker application takes the new vote and updates the persistent database which is a `PostgreSQL` in our case. The PostgreSQL simply has a table with a number of votes for each category. In this case, it increments the number of votes for either of them depending on which option user chooses to vote for. Finally the result of the vote is displayed in a web-interface which is another web application developed in Node.js. This resulting application reads the count of votes from the database and displays it to the user.

<img src="https://github.com/amandewatnitrr/kubernetes-tutorial/blob/master/imgs/micro3.png">

- So, let's now plan out what are the goals that we need to accomplish while setting up Microservices based Application with Kubernetes.
- Following are the Goals:
  - Deploying Containers
  - Enable Connectivity
  - External Access

- As we are aware of the fact that the smallest Kubernetes object that we can create is a POD. So, we must first deploy these applications as a POD  on our Kubernetes Cluster.
- For the sake of simplicity, we will stick with PODs. So, once the PODs are deployed, the next step is to enable connectivity b/w services. So, it's important to know connectivity requirements are. So we must be very clear about what application requires access to what services. We know that the redis database is accessed by the application is accessed by the voting app and the worker app. The Voting app sends the vote to the Redis Database and the Worker app reads the data from the redis database. The PostgreSQL database is accessed by the worker app to update it with the total count of votes and than it is further accessed by the result app to read the total count of votes to be displayed in the resulting page in the broeser. So we know that the voting app is accessed by the external users, the voters, and the result app is also accessed by the external users to view the results. So most of the components are being accessed by another component except for the worker app. Note that the worker app is not being accessed by anyone.

- Now we learned that a service can be used to expose an application to other applications or users for external access. So we will create a service for the each and every PODs to connect them to each other.

</strong>
</p>
