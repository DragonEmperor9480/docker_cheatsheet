# Docker Commands Cheat Sheet

This document provides a simple explanation of essential Docker commands, organized into logical sections for easy reference.

---

## Introduction
Docker is a platform for developing, shipping, and running applications in containers. 

Key Concepts:
- **Containers**: Lightweight, portable units that package an application and its dependencies.
- **Images**: Read-only templates used to create containers, containing the application code and libraries.
- **Docker Swarm**: A clustering and orchestration tool for managing a group of Docker engines.

This guide covers the most commonly used Docker commands.

---

## Basic Commands
These commands form the foundation of working with Docker:
- **Check Docker Version**:  
  `docker --version`  
  Verify the installed Docker version.

- **Run a Container**:  
  `docker run hello-world`  
  Run a container from an image. If the image is not available locally, it will be pulled from Docker Hub.

- **Name a Container**:  
  `docker run --name DragonEmperor9480 <image_name>`  
  Assign a specific name to a container.

- **Interactive Mode**:  
  `docker run -it <image_name>`  
  Run a container in interactive mode with a terminal.

- **Detached Mode**:  
  `docker run -d <image_name>`  
  Run a container in the background.

---

## Container Management
Containers are instances of Docker images. Use these commands to manage them:
- **Attach to a Container**:  
  `docker attach <container_id>`  
  Reattach to a running container.

- **Run for a Specific Time**:  
  `docker run <image_name> sleep 100`  
  Run a container for a specified duration before it exits.

- **List Running Containers**:  
  `docker ps`  
  Display all running containers.

- **List All Containers**:  
  `docker ps -a`  
  Display all containers (running and stopped).

- **Remove a Container**:  
  `docker rm <container_id>`  
  Delete a container.

- **Stop a Container**:  
  `docker stop <container_id>`  
  Stop a running container.

- **Inspect a Container**:  
  `docker inspect <container_id>`  
  View detailed information about a container.

---

## Image Management
Images are the building blocks of containers. These commands help you work with them:
- **Pull an Image**:  
  `docker pull <image_name>`  
  Download an image without running it.

- **List Images**:  
  `docker images`  
  Display all locally available images.

- **Remove an Image**:  
  `docker rmi <image_name>`  
  Delete an image.

---

## Running Commands in Containers
- **Execute a Command**:  
  `docker run ubuntu cat /etc/*release*`  
  Run a specific command inside a container.

- **Use a Specific Image Version**:  
  `docker run ubuntu:16.04`  
  Run a container using a specific version of an image.

---

## Resource Management
- **Limit CPU Usage**:  
  `docker run --cpu=.5 ubuntu`  
  Restrict a container to use no more than 50% of CPU.

- **Limit Memory Usage**:  
  `docker run --memory=100m ubuntu`  
  Restrict a container to use no more than 100MB of memory.

---

## Volumes and Data Persistence
- **Create a Volume**:  
  `docker volume create data_volume`  
  Create a persistent volume for storing data.

- **Mount a Volume**:  
  `docker run -v data_volume:/var/lib/mysql mysql`  
  Mount a volume to a container.

- **Mount a Directory**:  
  `docker run -v /data/mysql:/var/lib/mysql mysql`  
  Mount a specific directory from the host to a container.

- **New Mount Syntax**:  
  `docker run --mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql`  
  Use the newer syntax for mounting directories.

---

## Networking
- **List Networks**:  
  `docker network ls`  
  Display all Docker networks.

- **Inspect a Network**:  
  `docker network inspect bridge`  
  View detailed information about a network.

- **Default Networks**:  
  - `bridge`: Default network for containers.  
  - `none`: No network access.  
  - `host`: Use the host's network stack.

- **Create a Custom Network**:  
  ```bash
  docker network create \
    --driver bridge \
    --subnet 182.18.0.0/16 \
    custom-isolated-network
  ```  
  Create a user-defined network with a specific subnet.

- **Example: MySQL Network**:  
  ```bash
  docker network create \
    --driver bridge \
    --subnet 182.18.0.0/24 \
    --gateway 182.18.0.1 \
    wp-mysql-network
  ```  
  Create a network for a MySQL database.

- **Deploy MySQL**:  
  ```bash
  docker run --name mysql-db \
    -e MYSQL_ROOT_PASSWORD=db_pass123 \
    --network wp-mysql-network \
    mysql:5.6
  ```  
  Deploy a MySQL container attached to the custom network.

---

## Docker Swarm and Orchestration
Docker Swarm allows you to manage a cluster of Docker nodes as a single virtual system:
- **Initialize Swarm**:  
  `docker swarm init`  
  Initialize a Docker Swarm cluster.

- **Join Swarm**:  
  `docker swarm join --token <token>`  
  Join a worker node to the Swarm cluster.

- **Create a Service**:  
  `docker service create --replicas=3 my-web-server`  
  Deploy a service with multiple replicas.

---

## Storage Drivers
Storage drivers handle how Docker manages image layers and container filesystems. Supported drivers include:
- AUFS
- ZFS
- BTRFS
- Device Manager
- Overlay
- Overlay2

---

## Conclusion
This cheat sheet provides a quick reference for essential Docker commands. For more detailed information, refer to the official Docker documentation.
