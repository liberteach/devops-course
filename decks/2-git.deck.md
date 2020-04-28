---
title: Source Control Management (SCM) - Git
---

# DevOps course overview

1. Introduction to DevOps
2. **Source Control Management (SCM) - Git**
3. Continuous Testing, Continuous Integration & Continuous Delivery (CI/CD) - Travis CI and Heroku
4. Containers - Docker
5. Containers orchestration - Docker Compose
6. Containers orchestration - Kubernetes
7. Microservices & Service mesh - Istio
8. Infrastructure as code (IaC) - Ansible

A project at the end of the course.

gatsby-slide

# Source Control Management (SCM)

- History
  - Concept exists since 1950
  - Modern implementation since ~1980
  - Git in 2005
- Teamwork → Organisation
- May have seen [«Mercurial SCM»](https://www.mercurial-scm.org/) or [«Tortoise SVN»](https://tortoisesvn.net/)

gatsby-slide

# What do you manage ?

- Manage code, or any **text based** projects (like all the configuration needed for the project)
- Manage project versions
  - Global project version (tags)
  - Each modification is a «version»
- Manage change requests
- Keep track of changes and its authors
- Have multiple people working on your project

gatsby-slide

# Core concepts of Git

Learn git - https://git-scm.com/doc

- **Git Project** - regular folder tracked by git
- Each set of changes to files are **commits**
- Each commit has a **parent commit** (except for the first one)
- The current commit is the **HEAD**
- The git project is kept in a remote location - **repository**
- Retrieving changes from the repo is **pulling**
- Sending changes to the repo is **pushing**
- When choosing what to commit, files are **staged**

gatsby-slide

# Tags

So far:

- changes are managed, not the project
- all the commits come one after the other
- the only version available is the commit id

**Tagging** versions:

- Tag a **commit** to be a particular software version
- Easier to identify the versions
- You have to **push** the tags

gatsby-slide

# The source tree has brunches

- **Branches** - independent set of commits
- So far all the commits are on the **master** branch
- Branch can be an abstraction for line of development
  - **master** is the stable, tested version of the project
  - **dev** is the place where features come together
  - Branch can be temporary:
    - To have a change request
    - To develop an independent feature
- Create branches or switch between them with `git branch`

gatsby-slide

# Merge & conflicts

- Branches can be merged to have all the changes in only one branch
- «Change Request» → «Merge/Pull Request»
- When multiple changes are in conflict with each other, the merge fails: `Automatic merge failed; fix conflicts and then commit the result.`
- Solutions:
  - Cherrypick the changes (can be quite long)
  - Abandon your changes (and put them back later)
  - Work on the latest commit (git pull) and have a good task repartition

gatsby-slide

# Merge vs Rebase

Read this [article on Medium](https://medium.com/datadriveninvestor/git-rebase-vs-merge-cc5199edd77c).

# OpenSource Project Management

- Code managed by git, how can people contribute?
- **Fork** the project on your account
- Work on a change on your fork
- Ask for your changes to be added to the official code - [pull request](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests)

gatsby-slide

# Your work

1. [Duplicate a repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)

2. Try commands using their options:

- `git status`
- `git log`
- `git commit`
- `git tag`
- `git branch`
- `git push`
- `git fetch`
- `git pull`
- `git checkout`
- [Merge](https://git-scm.com/docs/git-merge)
- [Rebase](https://git-scm.com/docs/git-rebase)
- `git stash`
- `git squash`
