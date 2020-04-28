---
title: Infrastructure as code (IaC) - Ansible
---

# DevOps course overview

1. Introduction to DevOps
2. Source Control Management (SCM) - Git
3. Continuous Testing, Continuous Integration & Continuous Delivery (CI/CD) - Travis CI and Heroku
4. Containers - Docker
5. Containers orchestration - Docker Compose
6. Containers orchestration - Kubernetes
7. Microservices & Service mesh - Istio
8. **Infrastructure as code (IaC) - Ansible**

gatsby-slide

# Introduction

Ansible is a radically simple **IT automation engine** that automates:

  - cloud provisioning
  - configuration management
  - application deployment
  - intra-service orchestration
  - many other IT needs ...

## Videos

Watch in class:

- [What is Infrastructure as Code?](https://www.youtube.com/watch?v=zWw2wuiKd5o)
- [What is Ansible In Under 3 Minutes](https://www.youtube.com/watch?v=tWR1KXgEYxE) (3 min)
- [001 Introduction to Ansible](https://www.youtube.com/watch?v=GMzXAbT_wlk&list=PL4CwCXuy76Fe4Lll2ksYXGtupJNxpiBVV) (3 min)
- [002 Installing Ansible](https://www.youtube.com/watch?v=4xThcqDfbSA&list=PL4CwCXuy76Fe4Lll2ksYXGtupJNxpiBVV&index=2) (9 min)

Watch at home:

- [How Ansible works](https://www.youtube.com/watch?v=St__HLMZ8qQ)
- [Ansible: quick start video](https://www.ansible.com/resources/videos/quick-start-video)
- [Découvrir Ansible : outils d'orchestration et d'automatisation - ep01](https://www.youtube.com/watch?v=prtO-Ox8LW8)

gatsby-slide

# Your work

## Objectives

### Part 1

**Classwork:**

1. Configuring Ubuntu with Ansible (Katakoda scenario)

### Part 2

**Classwork:**

1. Prepare a virtual environment and install Ansible on it
2. Install Docker on VM
3. Run a docker container on VM (running Ansible manually)

**Homework, included to the project:**

4. Run a docker container using Volumes
5. Run docker containers using [docker_compose](https://docs.ansible.com/ansible/latest/modules/docker_compose_module.html) module

gatsby-slide

# Your work. Part 1

## 1. Configuring Ubuntu with Ansible (Katakoda scenario)

Follow the instructions of the [Katacoda scenario](https://www.katacoda.com/jonatanblue/scenarios/1).

gatsby-slide

# You work. Part 2

## Prerequisites

Before you can start the lab, you have to:

1. Install VirtualBox: https://www.virtualbox.org/wiki/Downloads
2. Install Vagrant on your computer: https://www.vagrantup.com/downloads.html
3. (Optional) **On Windows**, ensure that Hyper-V is disabled:
   1. Open a new PowerShell
   2. Run the following command:   
      ```
      Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All
      ```
4. Download the `centos/7` Vagrant box for the **Virtualbox provider**:

   ```
   $ vagrant box add centos/7
   ==> box: Loading metadata for box 'centos/7'
       box: URL: https://vagrantcloud.com/centos/7
   This box can work with multiple providers! The providers that it
   can work with are listed below. Please review the list and   choose
   the provider you will be working with.

   1) hyperv
   2) libvirt
   3) virtualbox
   4) vmware_desktop

   Enter your choice: 3
   ```

gatsby-slide

# Your work. Part 2 (classwork)

## 1. Prepare a virtual environment and install Ansible on it

Since Ansible can not be installed on Windows control node ([source](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements)), to avoid issues associated with the platform on which Ansible will be launched, we will use a virtual environment.

We will use the [`ansible_local` provisioner](https://www.vagrantup.com/docs/provisioning/ansible_local.html) what will install Ansible on [CentOS 7](https://www.centos.org/) Linux distribution virtual machine by [Vagrant](https://www.vagrantup.com/). So, you don't need Ansible on your computer!

The next step once you’ve installed Vagrant is to create a `Vagrantfile` and customize it to suit your needs. This is covered in detail in [the Vagrant documentation](https://www.vagrantup.com/docs/), and for this lab we will use a prepared `Vagrantfile`.

Take a look at the [`Vagrantfile`](../assets/lab-8-ansible/Vagrantfile) and at the YAML files [`playbooks/run.yml`](../assets/lab-8-ansible/playbooks/run.yml). To have more information how the `Vagrantfile` is configured follow this [Vagrant Guide](https://docs.ansible.com/ansible/latest/scenario_guides/guide_vagrant.html)

2. Create and provision the VM

```
cd assets/lab-8-ansible
vagrant up
```

3. Check that everything is ok by connecting to the VM through SSH:

```
vagrant ssh docker_server
```

gatsby-slide

# Your work. Part 2 (classwork)

## 2. Install Docker on VM

Take a look at the [playbooks/docker/install/tasks/main.yml](../assets/lab-8-ansible/playbooks/docker/install/tasks/main.yml)

1. Update the playbooks on the VM using `vagrant upload`:

```
vagrant upload playbooks /vagrant/playbooks docker_server
```

2. Rerun provisioning with the command:

```
vagrant provision
```

3. Check that Docker is installed on VM:

```
vagrant ssh docker_server
docker --version
```

It should print something like:

```
Docker version 19.03.8, build afacb8b
```

gatsby-slide

# Your work. Part 2 (classwork)

## 3. Run a docker container on VM (running Ansible manually)

1. Read [`playbooks/roles/docker/run/tasks/main.yml`](../assets/lab-8-ansible/playbooks/docker/run/tasks/main.yml) to understand how it relates.

This uses Ansible modules:
- [docker_image](https://docs.ansible.com/ansible/latest/modules/docker_image_module.html) - manage docker images
- [docker_container](https://docs.ansible.com/ansible/latest/modules/docker_container_module.html) - manage docker containers

2. Run the `docker/run` role

Connect to the VM using `vagrant ssh`

Run the playbooks using the right tag (replace `TAG`):

```
ansible-playbook /vagrant/playbooks/run.yml --tags TAG -i /tmp/vagrant-ansible/inventory/vagrant_ansible_local_inventory
```

3. Test your application by connecting to [`http://30.30.30.3`](http://30.30.30.3)

## Tip: How to copy Docker images from the host to Vagrant virtual machine without using a repository?

This can be useful if you already have an image on your laptop and you want to use the same image on you virtual host.

Instructions:

```
docker save -o <path for GENERATED tar file> <image name>
vagrant upload <path for GENERATED tar file> <path to TARGET tar file> <server name>
vagrant ssh docker_server
docker load -i <path to TARGET tar file>
```

Example:

```
docker save -o docker-img.tar sergkudinov/ece-userapi:latest
vagrant upload docker-img.tar /vagrant/docker-img.tar docker_server
vagrant ssh docker_server
docker load -i /vagrant/docker-img.tar
```

gatsby-slide

# Your work. Part 2 (homework, included to the project)

## 4. Run a docker container mounting Volumes

Find the instructions how to mount Volumes using the [docker_container module documentations](https://docs.ansible.com/ansible/latest/modules/docker_container_module.html).

## 5. Run docker containers using [docker_compose](https://docs.ansible.com/ansible/latest/modules/docker_compose_module.html) module.

## Results

All the configurations files should be commited to your project repository.
