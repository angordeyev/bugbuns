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

Copy the release:

```shell
docker cp ${CONTAINER}:/app ./_app
```

Or make as script:

```shell
image=$(docker build . -q --target builder)
container=$(docker run --detach ${image})
docker cp ${container}:/app ./_build/app
docker container rm ${container}
```

## Resources

* [Building Elixir/Phoenix Release With Docker. Kai.](https://kaiwern.com/posts/2020/06/20/building-elixir/phoenix-release-with-docker/)
