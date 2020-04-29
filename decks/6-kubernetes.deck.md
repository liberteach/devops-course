---
title: Containers orchestration - Kubernetes
---

# What is Container Orchestration?

**Container orchestration** automates the deployment, management, scaling, and networking of containers.

## It used for:

- Provisioning and deployment
- Configuration and scheduling
- Resource allocation
- Container availability
- Scaling or removing containers based on balancing workloads across your infrastructure
- Load balancing and traffic routing
- Monitoring container health
- Configuring applications based on the container in which they will run
- Keeping interactions between containers secure

## Videos:

- [Container Orchestration Explained](https://www.youtube.com/watch?v=kBF6Bvth0zw)

gatsby-slide

# Introduction to Kubernetes

**Kubernetes is** an open source container orchestration tool.

**Functions:**

- **automates** the distribution and scheduling of application containers across a cluster
- **coordinates** a highly available cluster of computers that are connected to work as a single unit.

**Advantages:**

- **is more efficient than past deployment models**, where applications were installed directly onto specific machines as packages deeply integrated into the host.

**Alternatives:**

- Docker Swarm
- Apache Mesos

gatsby-slide

# Resources

## Videos

- [Kubernetes Explained](https://www.youtube.com/watch?v=aSrqRSk43lY)
- [Kubernetes in 7 mins](https://www.youtube.com/watch?v=NChhdOZV4sY)
- [(Advanced) Kubernetes Deconstructed: Understanding Kubernetes by Breaking It Down](https://www.youtube.com/watch?v=90kZRyPcRZw)

## Links

- [Kubernetes official documentation](https://kubernetes.io/docs/home/)
- [Kubernetes concepts](https://kubernetes.io/docs/concepts/)
- [The Illustrated Children’s Guide to Kubernetes](https://www.cncf.io/the-childrens-illustrated-guide-to-kubernetes/)

## Tutorials

- [Katacoda course](https://www.katacoda.com/courses/kubernetes)
- [Learn Kubernetes Basics (official documentation)](https://kubernetes.io/docs/tutorials/kubernetes-basics/)

gatsby-slide

# Kubernetes clusters

A Kubernetes cluster consists of two types of resources:

- The **Master** coordinates the cluster
- **Nodes** are the workers that run applications

[Read more](https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro/#kubernetes-clusters)

gatsby-slide

# Kubernetes tools

We will use today these tools:

  1. [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) - runs a single-node Kubernetes cluster on your personal computer
  2. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) - Kubernetes command-line tool to run commands against Kubernetes clusters
  3. [Web UI (Dashboard)](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
  4. [Kompose (Kubernetes + Compose)](https://github.com/kubernetes/kompose) -  to help move `docker-compose` file to Kubernetes

[More Kubernetes tools](https://kubernetes.io/docs/reference/tools/)

gatsby-slide

# Your work

You will start a single node Kubernetes cluster using Minikube and deploy containerized applications on top of it.

## Objectives

**Part 1 (classwork):**

1. Installation
2. Quick start
3. Explore the local Kubernetes cluster

**Part 2 (homework, included to the project):**

4. Create an image of your app on Docker Hub
5. Deploy an app using `kubectl`
6. Deploy an app using Manifest yaml files

gatsby-slide

# Your work. Part 1

## 1. Installation

**Don't hesitate to read the full info on following pages!**

[Install Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/), this includes 3 steps:

  - [install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
  - [install a Hypervisor](https://kubernetes.io/docs/tasks/tools/install-minikube/#install-a-hypervisor)
  - [install Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/#install-minikube-using-chocolatey)

gatsby-slide

# Your work. Part 1

## 2. Quick start with Minikube

**Don't hesitate to read the full info on following pages!**

Follow the instructions on the [Quick start](https://kubernetes.io/docs/setup/learning-environment/minikube/#quickstart) page (only "Quickstart" section). Here you will:

  - `minikube start` - this command creates and configures a Virtual Machine that runs a single-node Kubernetes cluster. This command also configures your `kubectl` installation to communicate with this cluster.
  - create a Kubernetes Deployment
  - expose Deployment as a Service
  - explore pods
  - get the URL of the exposed Service (using an app)

gatsby-slide

# Your work. Part 1

## 3. Explore the local Kubernetes cluster

**Don't hesitate to read the full info on following pages!**

1. Explore the Kubernetes cluster using `kubectl` (use `kubectl --help` or its [overview](https://kubernetes.io/docs/reference/kubectl/overview/) to learn commands):

  - `kubectl cluster-info` - discover details of the cluster and its health status
  - `kubectl get nodes` - view the nodes in the cluster
  - `kubectl create deployment [OPTIONS]` - create deployment
  - `kubectl get pods` - status of the deployment can be discovered via the running Pods
  - ...

2. Explore the Kubernetes cluster via [Dashboard](https://kubernetes.io/docs/setup/learning-environment/minikube/#dashboard)

3. Explore Docker containers in the cluster [here](https://kubernetes.io/docs/setup/learning-environment/minikube/#use-local-images-by-re-using-the-docker-daemon):   
  - run `minikube docker-env` to work with the Docker daemon on your host (may work only on Mac/Linux)
  - then run, for example, `docker ps`

gatsby-slide

# Your work. Part 2

To do the part 2 you can be referenced to this tutorial - [Learn Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)

## 4. Create an image of your app on Docker Hub

1. Create an image:

```bash
cd path/to/your/project
docker build -t <username>/<imagename>:<tag> .
```

2. Create a repository on [Docker Hub](https://hub.docker.com/repositories). Try to configure automated builds connecting it to GitHub.

3. Push the image to Docker Hub

```bash
docker push <username>/<imagename>:<tag>
```

gatsby-slide

# Your work. Part 2

## 5. Deploy an app using `kubectl`

1. Create a Deployment
```bash
kubectl create deployment <your_deployment_name> --image=<username>/<imagename>:<tag>
```

2. To access your app Deployment, expose it as a Service:

```bash
kubectl expose deployment <your_deployment_name> --type=NodePort --port=<YOUR_PORT>
```

3. Explore docker containers and images, pods, deployments, services using:

- `docker ps`
- `kubectl`
- the Dashboard

4. Access to your app

Run a command `minikube service <your_deployment_name> --url` and navigate to the link.

gatsby-slide

# Your work. Part 2

## 6. Deploy an app using Manifest yaml files

**This is a part of the course project**

1. Use following resources to create a Manifest yaml files:

  - [Creating a Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment)
  - [Creating a Services](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service)
  - [Organizing resource configurations in one file](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#organizing-resource-configurations)

2. Run with `kubectl apply [OPTIONS]`

3. Commit new files to your GitHub. **Don't forget to update the README with usage instructions.**
