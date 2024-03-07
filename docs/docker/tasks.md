# Tasks

## Delete all unused containers, volumes, networks and images

```shell
docker system prune -a --volumes
```

## Open the Current Directory in a Container from a Repository Image

```shell
docker run -it --mount type=bind,source=$(pwd),target=/app -w /app --rm ubuntu
```

`--rm` - Automatically remove the container when it exits

## Open the Current Directory in a Container from a Dockerfile

```shell
docker run -it --mount type=bind,source=$(pwd),target=/app -w /app --rm $(docker build -q .)
```

`--rm` - Automatically remove the container when it exits

## Run a Dockerfile

```shell
docker run --rm $(docker build -q .)
```

## Attach Shell to a Running Container

First characters of container ID can be used

```shell
docker exec -it <container_name_or_id> bash
```

## Explore a Volume

```shell
docker run -it -v <volume_name>:/mnt/<volume_name> debian
```

## Run and Bind a Container to an IP Address

```shell
docker run -p 172.17.0.1:8000:5678 hashicorp/http-echo  -text="hello world"
```

```shell
curl -i 172.17.0.1:800
```

```output
HTTP/1.1 200 OK
...
```

```shell
curl -i 127.0.0.1:8000
```

```output
curl: (7) Failed to connect to 127.0.0.1 port 8000 after 0 ms: Couldn't connect to server
```
