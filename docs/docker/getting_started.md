# Getting Started

Press Tab after `docker stop ` or `dockser stop <first_letters>`
for command line autocompletion

Pull an image

    ➜ sudo docker image pull ubuntu

Run command using image container

    ➜ docker run ubuntu ls -la

Run container with interactive terminal

    ➜ docker run -it ubuntu

Run a web server, `-p <host_port:container_port>` is required

    ➜ docker run -p 80:80 nginx

Run MySQL server, `-e MYSQL_ALLOW_EMPTY_PASSWORD=true` sets the
required environment variable

    ➜ docker run -e MYSQL_ALLOW_EMPTY_PASSWORD=true -p 3306:3306 mysql

Exit a container and terminate

    ➜ exit

Exit a container without terminating it

    ➜ Ctrl-PQ

List running containers

    ➜ docker ps
    11ef884f8df6   ubuntu    "bash"    ...

Attach shell to running container, first characters of container ID can be used 

    ➜ docker exec -it <container_name_or_id> bash

Stop container 

    ➜ docker stop <container_name>

And see that the container is no longer running

    ➜ docker ps

But the container is still in the list with "exited" status

    ➜ docker ps -a
    CONTAINER ID   IMAGE ...               
    5ff3f26c9b43   ubuntu ...

Remove container

    ➜ docker rm 5f

The container no longer exists

    ➜ docker ps -a
    CONTAINER ID   IMAGE ...
