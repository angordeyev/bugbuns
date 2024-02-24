# Commands

## Command Line Autocompletion

**Example**

Press Tab after `docker stop` or `dockser stop <first_letters>`

## System

Run daemon:

```shell
systemctl start docker
```

Login:

```shell
docker login -u <dockerhub_user>
```

Clean disk space used by docker, it will delete volumes data:

```shell
docker system prune -a --volumes
```

## Containers

List containers:

```shell
docker ps
```

List all containers:

```shell
docker ps -a
```

Run a container (d - run in detache background mode, p - map ports):

```shell
docker run -dp <host_port>:<container_port> <image>
```

Run a named container (d - run in detache background mode, p - map ports):

```shell
docker run --name <container name> -dp <host port>:<container port> <image>
```

Stop a container:

```shell
docker stop <container name or ID>
```

Remove a container:

```shell
docker rm <container name or ID>
```

Remove a container and stop it if running

```shell
docker rm -f <container name or ID> # stop if a container is running and remove
```

Execute a command in a container:

```shell
docker exec <container name or ID> ls -la
```

Go to a container shell (i = interactive, t = TTY):

```shell
docker exec -it <container-id> bash
```

## Volumes

List volumes:

```shell
docker volume ls
```

Run a container with a mounted volume:

```shell
docker run -dp <host_port>:<container_port> -v <volume>:</mount/path> <image>
```

Inspect a volume:

```shell
docker volume inspect <volume_name>
```

Remove all volumes:

```shell
docker volume prune
```

## Command Aliases

Pull images:

```shell
docker image pull ubuntu
docker pull ubuntu
```

List images:

```shell
docker images
docker image ls
```

List containers:

```shell
docker ps
docker container ls
```
