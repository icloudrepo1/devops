# What is Docker Swarm ?

Docker Swarm is a native clustering and orchestration tool for Docker containers. 

It enables you to manage a group of Docker nodes as a single virtual system, simplifying container deployments and scaling. 

Swarm mode is built into Docker, making it an attractive choice for teams already using Docker. We have to deploy the application on cluster.


### What is Cluster ?


In Docker Swarm, a cluster is a group of multiple Docker nodes that work together as a single system to run containerized applications.

A Swarm cluster consists of :-

#### Manager Nodes – Control and manage the cluster and services.

#### Worker Nodes – Run the application containers.

The manager node assigns tasks to worker nodes, ensuring high availability and scalability. This allows applications to run smoothly even if some nodes fail.


# How to create a cluster in Docker Swarm ?


Let’s walk through a real-world scenario where we deploy a multi-node Docker Swarm cluster.

#### step-1 :

Launch 3 EC2 Instances (1 Master, 2 Worker Nodes). Ex- Amazon Linux 2023 AMI, t2.micro


#### step-2 :

Connect 3 EC2 Instances

Lets install docker on each node

```
yum install docker -y && systemctl start docker
```


#### step-3 :

Initialize the Swarm on Master

```
docker swarm init
```


This command initializes Swarm mode and generates a token. If we copy the token and paste it on worker node, then the worker node will join in the docker swarm cluster.


#### step-4 :

On the manager node, check the status of the cluster

```
docker node ls
```


You should see a list of all nodes in the cluster.


# Deploying a Service in Docker Swarm


#### step-5 :

Let’s deploy a simple application across the cluster. (process it - master)

```
docker service create --name DEVBABU --replicas 3 -p 8080:80 icloudrepo1/dswarmwebapp:v1
```

(SERVICE-NAME ---> DEVBABU)

(COPY INSTANCES IP ALONG WITH 8080)


To check if the service is running

```
docker service ls
```


To see details of running tasks (containers)

```
docker service ps DEVBABU
```


Scaling is effortless in Swarm. If traffic increases, you can scale up


```
docker service scale DEVBABU=5
```

(EX- 5(containers))



To stop or remove a Docker service

```
docker service rm DEVBABU
```


#### step-6 :


##### Rolling Updates in Docker Swarm

Imagine you need to update your application to a newer version. Instead of taking everything down, Swarm allows rolling updates.

```
sudo docker service update --image icloudrepo1/latestdsapp:v2 DEVBABU
```


(COPY INSTANCES IP ALONG WITH 8080)


##### Rollback in Docker Swarm

```
docker service rollback DEVBABU
```


Now check the output, you can see the old output in browser.


##### Cluster Maintenance in Docker Swarm


To remove a node from cluster, go to that worker node and perform the below command

```
docker swarm leave
```


Now remove the node from the cluster

```
docker node rm <node-id>
```


If you want to add a worker node to our cluster, copy the token and paste it on any docker host. It will join as a worker node in your cluster.



----------END-------------

