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
