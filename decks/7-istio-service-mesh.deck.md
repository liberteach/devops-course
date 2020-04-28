---
title: Microservices & Service mesh - Istio
---

# DevOps course overview

1. Introduction to DevOps
2. Source Control Management (SCM) - Git
3. Continuous Testing, Continuous Integration & Continuous Delivery (CI/CD) - Travis CI and Heroku
4. Containers - Docker
5. Containers orchestration - Docker Compose
6. Containers orchestration - Kubernetes
7. **Microservices & Service mesh - Istio**
8. Infrastructure as code (IaC) - Ansible

gatsby-slide

# Microservices architecture

**Microservices (microservice architecture)** - a style that structures an application as a collection of services that are:

- Highly maintainable and testable
- Loosely coupled
- Independently deployable
- Organized around business capabilities
- Owned by a small team

## Monolithic architecture (old school)

**Monolith means composed all in one piece.** The Monolithic application describes a single-tiered software application in which different components combined into a single program from a single platform.

## Videos:
  - [Comprendre les microservices en 6 minutes](https://www.youtube.com/watch?v=ucHwp1jUS2w) (6 min)
  - Microservices vs Monolithic - [What are Microservices?](https://www.youtube.com/watch?v=CdBtNQZH8a4) (7 min)

gatsby-slide

# Service mesh

**Service mesh** - an infrastructure layer for facilitating service-to-service communications between microservices, often using a **sidecar proxy**.

**Provides:**

  - Connection between microservices
  - Observability into communications
  - Secure
  - Control

## Platforms implementing a service mesh:

  - Istio
  - Consul
  - Linkerd
  - ...

## Videos

  - [Service Mesh : l'essentiel en 4 minutes (avec Istio)](https://www.youtube.com/watch?v=o6Zh6AaeYXw) (4 min)
  - [What is a service mesh](https://www.youtube.com/watch?v=vh1YtWjfcyk&t=38s) (10 min)
  - An excellent presentation - [Demystifying Service Mesh](https://www.youtube.com/watch?v=bEFILWrRJJ4) (36 min)

gatsby-slide

# Istio

**Istio** - a platform that does a service mesh (provides a uniform way to secure, connect, and monitor microservices).

**Provides operational requirements:**

  - A/B testing
  - canary rollout (deployment)
  - rate limiting
  - access control
  - end-to-end authentication

## Videos

  - [What is Istio?](https://www.youtube.com/watch?v=1iyFq2VaL5Y) (4 min)
  - [Istio Service Mesh Explained](https://www.youtube.com/watch?v=6zDrLvpfCK4) (5 min)
  - Representing a canary rollout - [Kubernetes drone demo: Using Istio to manage app traffic](https://www.youtube.com/watch?v=QTD-gqS2E7w) (2 min)

## Links

  - [Official website](https://istio.io/)
  - [What is Istio?](https://istio.io/docs/concepts/what-is-istio/)

gatsby-slide

# You work

## Objectives

**Part 1 (classwork):**

1. Quick start with Istio
2. Route requests
3. Traffic shifting (canary rollout)

**Part 2 (homework, included to the project):**

4. Deploy your application
5. Route requests between 2 versions
6. Traffic shifting 2 versions

gatsby-slide

# You work. Part 1

## 1. Quick start with Istio

This task lets you quickly evaluate Istio.

### Instructions

1. [Install Minikube and start a Kubernetes cluster](https://istio.io/docs/setup/platform-setup/minikube/)

After Minikube installation run:

  - `minikube config set vm-driver virtualbox` (or `vmware`, or `kvm2`)
  - `minikube start --memory=16384 --cpus=4 --kubernetes-version=v1.18.0`

2. [Install Istio](https://istio.io/docs/setup/getting-started/)

Do everything up to the [Next steps](https://istio.io/docs/setup/getting-started/#next-steps) section.

### The results

  - running [Bookinfo example application](https://istio.io/docs/examples/bookinfo/) and available at `http://$GATEWAY_URL/productpage` (where $GATEWAY_URL - is specific IP and PORT for every deployment)
  - running [Kiali dashboard](https://kiali.io/) with an overview of your mesh with the relationships between the services, like on [this image](https://istio.io/docs/setup/getting-started/kiali-example2.png).

gatsby-slide

# You work. Part 1

## 2. Request Routing

This task shows you how to route requests dynamically to multiple versions of a microservice.

### Instructions

- [Request routing](https://istio.io/docs/tasks/traffic-management/request-routing/)

### The results

  - sending 100% of the traffic to the `v1` version of each of the Bookinfo services
  - setting a rule to selectively send traffic to version `v2` of the reviews service based on a custom `end-user` header

gatsby-slide

# You work. Part 1

## 3. Traffic Shifting (canary rollout)

This task shows you how to gradually migrate traffic from an older version to a new version.

### Instructions

- [Traffic shifting](https://istio.io/docs/tasks/traffic-management/traffic-shifting/)

### The results

  - migrating traffic from an old to new version of the `reviews` service using Istio’s weighted routing feature

gatsby-slide

# You work. Part 2

4. Deploy your application
5. Route requests between 2 versions of the app
6. Traffic shifting between 2 versions

### The results

  - Yaml deployments files pushed to git repository
