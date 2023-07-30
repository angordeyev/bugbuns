# Tasks

## Delete all unused containers, volumes, networks and images

```sh
docker system prune -a --volumes
```

## Open the Current Directory in a Container from an Image

```sh
docker run -it --mount type=bind,source=$(pwd),target=/app -w /app ubuntu --rm
```

`--rm` - Automatically remove the container when it exits


## Run a Dockerfile

```sh
docker run --rm $(docker build -q .)
```
