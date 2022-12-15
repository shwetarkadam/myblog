+++
title = "Tackling procrastination and kubernetes study"
author = ["Shweta Kadam"]
date = 2022-02-25T15:45:00+05:30
tags = ["kubernetes", "basics", "blog", "notes", "learning", "kubeapiserver"]
draft = false
+++

After a long series of procrastination and getting the hit of motivation from reading Atomic Habits(great book which I recommend others) ,I’m finally learning kubernetes basics.As a motivator to get better at writing and publish more posts as well as learn kubernetes.I have decided to publish 1 article every Sunday.I would like to post 2 posts per week but I want to start small and consistent. Once again I’m treating my blog as a journal to showcase how much I actually understand kubernetes.Also its quite handy to have my own notes on a site. So here is a blog post on kubernetes basics part 1.This will be a multi part series. Before we begin some pre requisites which one needs to know :-


## Pre requisite {#pre-requisite}

You should be already familiar and comfortable with the concept of containers and container run-time such as docker as kubernetes is for managing different containers and their deployment at a large scale.Another point which is not mandatory but good to know would be basic docker commands like docker run etc.


## What is kubernetes? {#what-is-kubernetes}

Kubernetes is an open-source technology that is used for container orchestration. And what is container orchestration exactly? It is the process of continuous deployment ,scaling and management of containers.

Lets first look at the kubernetes architecture and the individual components in it.


## Node: {#node}

A Node is either a physical or virtual machine on wihc kubernetes is installed. A node is like a worker machine on which containers (having our application) will be running by Kubernetes.And like any other machine ,nodes can crash for a number of reasons ;) .So once the node crashes the application will be go down as well. So tackle this we need multiple nodes rather than 1 node.

And mulitple nodes come together to form a group known as the cluster.So even if one node inside the cluster fails,we have our application accessible and running from the other nodes.Plus it helps in sharing load!


## \* Master Node : {#master-node}

So now we have our cluster running on a group of nodes which are running our containerised apps.But who is responsible to manage this cluster:?Also when a node goes down how to direct the traffic of the failed node to other working nodes?Also who stores the information about these worker nodes stored? and How are the nodes monitored?

The master node!

The master node is another machine with kubernetes installed in it and it watches over the nodes and does the actusl orchestration of the worker nodes.

> Note that a cluster can have multiple master nodes depending on the size of the cluster.

because at the end of the day , a master node is a machine (which can crash) and for high availability we need to avoid that.


## Other components: {#other-components}

When you install kubernetes in your system,you are actually installing the follwing components:

-   An Kube api server (Master)
-   An etcd service (Master)

-A kubelet service (Worker)

-   Controller (Master)
-   Scheduler (Master)
-   Container Runtime


## Kube API server: {#kube-api-server}

Kubeapi server acts as a frontend for kubernetes.The users,commandline tools,managment devices all interact with the cluster via the Kube API server.


## etcd {#etcd}

etcd is a distributed key value store used to store data about how to manage the cluster.It is also resp0onsible to implement logs within the cluster to ensure there is no conflict between mulitple masters.

> Note that your application data is not stored in etcd only logs and information about the cluster.


## Scheduler {#scheduler}

Scheduler is responsible is distributing containers across multiple nodes.It looks for newly created containers and assigns them to nodes.


## Controllers {#controllers}

Controllers are the brain behind the orchestration. They are responsible for notcining and responding nodes,containers or endpoint goes down.The controller takes decsions to bring up new nodes in this case.


## Container Runtime {#container-runtime}

The container runtime is the underying software that runs the containers.Most of the times,its docker.I have used docker but there are other runtimes such as CRI-O


## KubeletPermalink {#kubeletpermalink}

Kubelet is an agent that runs on each worker node in the cluster. The agent is in charge of making sure that containers are running on the nodes as expected.


## Master vs Worker nodesPermalink {#master-vs-worker-nodespermalink}

So now we know there are 2 types of nodes : Masternode and Worker node. How does a node become master or a worker node? A worker node has the containers are hosted and running .Hence to run these containers we need a Container Runtime such as docker installed in these machines.

The master has a kube API server and this is what differentiates the master from worker nodes. The worker node have the kubelet agent that interacts with the master to proivide health information about the worker nodes and carries out the instrcutions given by the master node on worker nodes.The master has all this information stored in key value store (etcd) known as the etcd.The master also has the controller and scheduler.


## KubectlPermalink {#kubectlpermalink}

kubectl is a commandline tool is used to deploy and manage applications in a cluster.Basically we are going to use these commands from the kubectl tool to get us information (kubectl get,status describe) about the nodes and other components in the cluster and to manage many other operations.

`kubectl run` –Used to deploy an application onto the cluster

`kubectl get cluster-info` –Used to fetch the cluster information

`kubectl get nodes` –Used to fetch information about nodes.

That is all on basic overview.Next article will be focused on pod and how pods work in nodes in kubernetes.
