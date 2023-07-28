# Commands

## Command Line Autocompletion

**Example**

Press Tab after `docker stop` or `dockser stop <first_letters>`

## System

Run daemon

    ➜ systemctl start docker

Login

    ➜ docker login -u <dockerhub_user>

Clean disk space used by docker

    ➜ docker system prune

## Images

Pull an image with the default tag

    ➜ docker pull alpine

Pull an image with tag

    ➜ docker image pull ubuntu:latest

List local images

    ➜ docker images
    ubuntu                    latest      2dc39ba059dc   2 weeks ago    77.8MB
    alpine                    latest      9c6f07244728   6 weeks ago    5.54MB

Build image for the Docker file in the current folder, "-t" sets the image tag

    ➜ docker build -t getting-started .

Show image layers

    ➜ docker image history <image>

Change tag for the image to push on dockerhub

    ➜ docker tag getting-started <dockerhub_user>/getting-started

Push to the repository

    ➜ docker push <repository_path>

Run a command using an image

    ➜ docker run alpine echo "hello"

Run multiple commands using an image

    ➜ docker run alpine echo "hello" && echo "world"

## Containers

List containers

    ➜ docker ps

List all containers

    ➜ docker ps -a

Run container (d - run in detache background mode, p - map ports)

    ➜ docker run -dp <host_port>:<container_port> <image>

Run named container (d - run in detache background mode, p - map ports)

    ➜ docker run --name <container name> -dp <host port>:<container port> <image>

Stop a container

    ➜ docker stop <container name or ID>

Remove a container

    ➜ docker rm <container name or ID>

Remove a container and stop it if running

    ➜ docker rm -f <container name or ID> # stop if a container is running and remove

Execute command in a container

    ➜ docker exec <container name or ID> ls -la

Go to a container shell (i = interactive, t = TTY)

    ➜ docker exec -it <container-id> bash 

## Volumes

List volumes

    ➜ docker volume ls

Run container with a mounted volume

    ➜ docker run -dp <host_port>:<container_port> -v <volume>:</mount/path> <image>

Inspect volume

    ➜ docker volume inspect <volume_name>

## Command Aliases

Pull images

    ➜ docker image pull ubuntu
    ➜ docker pull ubuntu

List images

    ➜ docker images
    ➜ docker image ls

List containers

    ➜ docker ps
    ➜ docker container ls
