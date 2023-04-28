# Containers

Container name or container Id can be used when referencing a container.

## Run

Run a container (d - run in detache background mode, p - map ports) from an image
 
    docker run -dp <host_port>:<container_port> <image>

Run a named container (d - run in detache background mode, p - map ports) from an image

    docker run --name <container_name> -dp <host_port>:<container_port> <image>

Stop a container

    docker stop <container>

## List

List containers (ps - process status)

    docker ps

    docker container ls

List all containers

    docker ps -a

List container IDs

    docker ps -q

## Remove

Remove a container

    docker rm <container>

Remove a container and stop it if running

    docker rm -f <container>

Remove all stopped containers

    docker container prune

Remove all containers (f = force, q = list container IDs only)

    docker container rm -f $(docker ps -q)

## Execute Commands

Create a container from an image and go to terminal (i = interactive, t = TTY)

    docker run -it <image> bash

Create a container from an image and run a command

    docker run <image> ls -la

Execute command in a container

    docker exec <container name or ID> ls -la

Go to a container shell (i = interactive, t = TTY)

    docker exec -it <container name or ID> bash

## Attach

Run a named container

    docker run -it --name ubuntu_container ubuntu

Attach to the container

    docker attach ubuntu_container

## Send STDIN

    echo 'test' | socat EXEC:"docker attach vector",pty STDIN
