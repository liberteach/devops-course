---
title: Containers - Docker
---

# Introduction to Docker

Container - is a running process, with some added encapsulation features.

## Provides

  - developing lots of small changes
  - shipping easily
  - running everywhere

## Videos

  - [Introduction To Docker and Docker Containers](https://www.youtube.com/watch?v=JSLpG_spOBM) (8 min)
  - [Docker Client, Images and Containers](https://www.youtube.com/watch?v=CcxbHkqzJuI) (14 min)
  - [Docker : l'essentiel en 7 minutes](https://www.youtube.com/watch?v=caXHwYC3tq8&t=1s) (7 min)

## Links

  - [About](https://docs.docker.com/engine/)
  - [Overview](https://docs.docker.com/engine/docker-overview/)
  - [Get started](https://docs.docker.com/get-started/)

gatsby-slide

# Docker Architecture

[Image - Docker objects and Docker engine](https://docs.docker.com/engine/images/engine-components-flow.png)

## Docker Engine

- Server (daemon process)
- REST API
- Client (CLI)

## Docker objects

- Images
- Containers
- Networks
- Volumes
- ... some more objects

They all are available to be observed and controlled using the command `docker <object-name>`.

## Architecture

[Image - Docker architecture](https://docs.docker.com/engine/images/architecture.svg)

- client (CLI via REST API)
- server (Docker host) - deamon, containers, images, volumes
- registry - Docker Hub

gatsby-slide

# Development Scenario

1. Developers write code and share their work using Docker containers
2. Developers use Docker to push their applications into a **test environment** and execute automated and manual tests
3. Developers find bugs, they fix them in the **development environment** and redeploy to the **test environment**
4. When testing is complete, getting the fix to the customer is as simple as pushing the updated image to the **production environment**

gatsby-slide

# CLI commands

CLI uses Docker RESR API - https://docs.docker.com/develop/sdk/examples/

- `docker help`
- `docker ps` - list containers
- `docker container`
- `docker image`
- `docker volume`
- `docker networks`
- `docker system` - info
- `docker run` - run a command in a new container
- `docker exec` - run a command in a running container

Example: `docker run -i -t ubuntu /bin/bash`

gatsby-slide

# Building Docker images

`Dockerfile` - configuration file for building images.

**Python:**
```
FROM ubuntu:15.04
COPY . /app
RUN make /app
CMD python /app/app.py
```

**Node.js:**
```
FROM node:12
WORKDIR /usr/src/app
COPY package.json .
RUN npm install
COPY . .
CMD [ "npm", "start" ]
```

To exclude some files from the docker we use [`.dockerignore` file](https://docs.docker.com/engine/reference/builder/#dockerignore-file)

gatsby-slide

# Storage

Overview - https://docs.docker.com/storage/

Storage types:

  - volume - https://docs.docker.com/storage/volumes/
  - bind mount - https://docs.docker.com/storage/bind-mounts/
  - tmpfs mount - https://docs.docker.com/storage/tmpfs/

gatsby-slide

# Your work (included to project)

## 1. Build a docker image and run a container

**1. Configure the Docker image**

Create a `Dockerfile` (without any extension) under the root of your project.

Example:

```
FROM node:12

WORKDIR /usr/src/app
COPY package.json .
RUN npm install
COPY . .

EXPOSE 3000
CMD [ "npm", "start" ]
```

**2. Build a docker image (don't forget a dot at the end of the command)**

```
docker build -t <docker-account-name>/<custom-image-name> .
```

**3. Run docker container**

```
docker run -p <PORT_1>:<PORT_2> <docker-account-name>/<custom-image-name>
```

Binding ports ([more info](https://runnable.com/docker/binding-docker-ports)):

- `PORT_1` - an external port which will be listened by you host
- `PORT_2` - en internal port inside the container

**4. Test your running app on `http://localhost:<PORT_1>`**

gatsby-slide


# Your work (included to project)

## 2. Use docker volumes

1. Run your docker container with the option `-v`

```
docker run -p [PORT_1]:[PORT_2] -v <path_to_dir_on_your_host>:<path_to_dir_inside_container> <your name>/<image name>
```

Binding volumes ([more info](https://docs.docker.com/storage/bind-mounts/)):

- `path_to_dir_on_your_host` - where you want to allocate your file storage
- `path_to_dir_inside_container` - where is located your storage inside the container

2. Test your running app on `http://localhost:<PORT_1>`

3. Create users and check your storage directory `path_to_dir_on_your_host`

4. Run one more container with different `PORT_1` and the same `path_to_dir_on_your_host`, then test how the both containers are shearing one volume.
