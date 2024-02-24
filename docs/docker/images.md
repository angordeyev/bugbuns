# Images

## Commands

Pull an image with the default tag:

```shell
docker pull alpine
```

Pull an image with tag:

```shell
docker image pull ubuntu:latest
```

List local images:

```shell
docker image ls
```
```output
    ubuntu                    latest      2dc39ba059dc   2 weeks ago    77.8MB
    alpine                    latest      9c6f07244728   6 weeks ago    5.54MB
```

Show image layers:

```shell
docker image history <image>
```

Build image for the Docker file in the current folder, "-t" sets the image tag:

```shell
docker build -t getting-started .
```

Change tag for the image to push on DockerHub:

```shell
docker tag getting-started <dockerhub_user>/getting-started
```

Push to the repository:

```shell
docker push <repository_path>
```

Run a command using an image:

```shell
docker run alpine echo "hello"
```

Run multiple commands using an image:

```shell
docker run alpine echo "hello" && echo "world"
```

## Dockerfile

### Arguments


