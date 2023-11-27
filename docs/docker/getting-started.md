# Getting Started

Pull an image:

```shell
sudo docker image pull ubuntu
```

Run command in container:

```shell
docker run ubuntu ls -la
```

Run container with interactive terminal:

```shell
docker run -it ubuntu
```

Exit a container and terminate:

```shell
exit
```

Exit a container without terminating it:

```shell
Ctrl-PQ
```

List running containers:

```shell
docker ps
```
```output
    11ef884f8df6   ubuntu    "bash"    ...
```

Attach shell to running container, first characters of container ID can be used:

```shell
docker exec -it <container_name_or_id> bash
```

Stop a container:

```shell
docker stop <container_name_or_id>
```

And see that the container is no longer running:

```shell
docker ps
```

But the container is still in the list with "exited" status:

```shell
docker ps -a
```
```output
    CONTAINER ID   IMAGE ...
    5ff3f26c9b43   ubuntu ...
```

Remove the container:

```shell
docker rm 5f
```

Check the container no longer exists:

```shell
docker ps -a
```
```output
    CONTAINER ID   IMAGE ...
```
