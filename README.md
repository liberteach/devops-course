# Learning DevOps tools

Modules:

1. Introduction to DevOps
2. Source Control Management (SCM) - Git
3. Continuous Testing, Continuous Integration & Continuous Delivery (CI/CD) - Travis CI and Heroku
4. Containers - Docker
5. Containers orchestration - Docker Compose
6. Containers orchestration - Kubernetes
7. Microservices & Service mesh - Istio
8. Infrastructure as code (IaC) - Ansible

## Prerequisites

Learning DevOps tools requires familiarity with command line interface (CLI) usage and to having basic programming skills.

For Windows users it is recommended to use [Git Bash](https://gitforwindows.org/) instead of regular CMD to have commands like in LINUX and UNIX environments.

## Usage

### 1. Reading slides' content

Slides content can be easily read directly on GitHub in the [decks](decks) folder.

### 2. Website on Netlify

The slides are available on Netlify as a static website - [devops-course.netlify.app](https://devops-course.netlify.app/).

[![Netlify Status](https://api.netlify.com/api/v1/badges/53585012-d83b-481f-856c-c5c2560b7a74/deploy-status)](https://app.netlify.com/sites/devops-course/deploys)

### 3. Build slides locally as a static website

You can also build a static website and read slides in a browser.

This project uses [Gatsby.js](https://www.gatsbyjs.org/) framework and requires [Node.js](https://nodejs.org/en/) installed. To build and run slides on your local run:

```
git clone https://github.com/liberteach/devops.git
cd devops
npm install
npm run serve
```

Then open `http://localhost:9000` (could be another port number) in a browser.

## Content description

- [decks](decks) - slide's content
- [assets](assets) - materials and code examples

## Author

Sergei Kudinov   
sergei@adaltas.com   
Developer and Data Engineer at [Adaltas](https://www.adaltas.com/)
