# Docker

Generate a new Phoenix application:

```shell
mix phx.new --install --no-ecto phoenix_docker_release
```

Generate relase files:

```shell
mix phx.gen.release --docker
```

Build builder image:

```shell
IMAGE=$(docker build . -q --target builder)
```

Make a temporary conatainer:

```shell
CONTAINER=$(docker run --detach ${IMAGE})
```

Create the release folder:

```shell
mkdir -p _build/prod/rel/<release_name>
```

Copy the release:

```shell
docker cp ${CONTAINER}:/app/_build/prod/rel/<release_name> _build/prod/rel
```

## Scripts

Build a release using the default Dockerfile:

```shell
# Relase name is the application name if not set explicitly
rel_name=<release_name>
rel_directory="_build/prod/rel"
image=$(docker build -q --target builder .)
container=$(docker run --detach ${image})
mkdir -p ${rel_directory}
docker cp ${container}:/app/${rel_directory}/${rel_name} ${rel_directory}
docker container rm ${container}
```

Build a release using the default Dockerfile and a custom image:

```shell
rel_name=<release_name>
rel_directory="_build/prod/rel"
image=$(docker build -q --target builder .)
container=$(docker run --detach ${image})
mkdir -p ${rel_directory}
docker cp ${container}:/app/${rel_directory}/${rel_name} ${rel_directory}
docker container rm ${container}
```

```shell
rel_name=<release_name>
builder_image=<builder_image>
rel_directory="_build/prod/rel"
image=$(docker build --build-arg builder_image=${builder_image} -q --target builder .)
container=$(docker run --detach ${image})
mkdir -p ${rel_directory}
docker cp ${container}:/app/${rel_directory}/${rel_name} ${rel_directory}
docker container rm ${container}
```

## Resources

* [Building Elixir/Phoenix Release With Docker. Kai.](https://kaiwern.com/posts/2020/06/20/building-elixir/phoenix-release-with-docker/)
