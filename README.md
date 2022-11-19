# Learning K8s concepts and basic workings

## What is kubernetes orchestrator?

- This is an entertaining comic to know about K8s. [here](https://cloud.google.com/kubernetes-engine/kubernetes-comic/)
- K8s is a popular container orchestration tool that allows us to manage and deploy multiple containers that interact with each other in a coordinated way.
- It is aimed at production systems. It was designed to be able to control big deployments and to abstract most of the infrastructure's details.
- Every element that we see in a cluster is configured programmatically and k8s is smart enough to manage where to  deploy clusters based on the capacity that's available

### Why not just use docker-compose?

- Docker compose can also orchestrate different containers and coordindate them but it does so without dealing with multiple servers.

## But there is docker swarm too

- Although docker swarm is easier to setup than kubernetes, assuming that we have to manage the servers, k8s is more powerful and customizable.
- K8s also has a bigger community and higher pace of innovation. It's also better at handling issues.

## 0. Set-up K3s (OPTIONAL)

### K3s

- K3s is a minimalistic installation of kubernetes that we can use to run a cluster contained in a single binary.

### Installation

- `curl -sfL https://get.k3s.io | sh -`: Install k3s

- `sudo systemctl edit --ful k3s.service` Restart k3s in docker mode
  - replace `ExecStart=/usr/local/bin/k3s server` with `ExecStart=/usr/local/bin/k3s server --docker`

- if k3s not started
  - `sudo systemctl daemon-reload`
  - `sudo systemctl restart k3s`
  - `sudo systemctl enable k3s`

- Allow access outside of root to `kubectl` config
  - `sudo chmod 644 /etc/rancher/k3s/k3s.yaml`

- if ur user isn't in the docker group add them to be able to run docker commands
  - `sudo usermod -aG docker $USER`
  - Sometimes we may need to log out and log in again for the group effect to take place

- [Install kubectl](https://kubernetes.io/docs/tasks/tools/)
  - kubectl commands controll kubernetes operation

## 0. TRY MINIKUBE (Either this or k3s)

### Minikube Installation

- [Install](https://minikube.sigs.k8s.io/docs/start/)

### Commands to run

- `minikube start` to start our cluster

## Understanding the different kubernetes elements

### 1. Pods

- Pods are the smallest building block in kubernetes object model. The pod "sees" the container but the k8s only see the pod. So, there's a level of abstraction there.
- Most pods hold just one container though tightly-coupled processes will sometimes share a pod.

### 1. Nodes

- Groups of pods are located on a single machine (real or virtual). Each of which we call a node.
- Nodes are then grouped into clusters.
- Each of the cluster is overseen by a master node (most cloud provider provide this one for free)
- Nodes create a network between them that routes all the requests that have been addressed to the cluster so that any request that's sent to any node in the cluster will be answered adequately.
- K8s will handle what deployable goes to what node.
- It even recovers nodes if they go down or moving them around from one node to another if there are any resource issues.
- These are the backbones that support the cluster.

### 2. Deployment

- Clusters are put in place by deployment (a simple yaml file).
- It's a simple yaml file that tells about the processes that we want up and running to do our work.

## Features of k8s

- K8s then selects the machine and propagates the containers in each pod, pulling down the container images specified in the deployment
- By the power of the kubernetes abstraction we have power of interchangeable container replicas and interchangeable machines.
- K8s will properly utilize the resources.
- It is self-healing
  - system compares the ideal state as expressed in the deployment to the actual state of pods and clusters in real operation and tries to attain it.
- If there are any violation or inconsistency than that something is terminated and instantly reborn
