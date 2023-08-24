# Tasks

## Delete all unused containers, volumes, networks and images

```sh
docker system prune -a --volumes
```

## Open the Current Directory in a Container from a Repository Image

```sh
docker run -it --mount type=bind,source=$(pwd),target=/app -w /app --rm ubuntu
```

`--rm` - Automatically remove the container when it exits


## Open the Current Directory in a Container from a Dockerfile

```sh
docker run -it --mount type=bind,source=$(pwd),target=/app -w /app --rm $(docker build -q .)
```

`--rm` - Automatically remove the container when it exits

## Run a Dockerfile

```sh
docker run --rm $(docker build -q .)
```


## Attach Shell to a Running Container

First characters of container ID can be used

```sh
docker exec -it <container_name_or_id> bash
```
