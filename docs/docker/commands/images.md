# Images

## Commands

### Frequently Used

Pull an image with the default tag

    docker pull alpine

Pull an image with tag

    docker pull ubuntu:latest 

Push docker image to repository
 
    docker image push <repository_name>

List local images

```sh
docker images
```
```output
ubuntu                    latest      2dc39ba059dc   2 weeks ago    77.8MB
alpine                    latest      9c6f07244728   6 weeks ago    5.54MB
```

Seach docker images 

    ➜ docker search ubun
    NAME               DESCRIPTION 
    ubuntu             Ubuntu is a Debian-based Linux operating sys… 
    ubuntu-upstart     DEPRECATED, as is Upstart (find other proces…

Build image for the Docker file in the current folder, "-t" sets the image name and an 
optional tag

    ➜ docker build -t <repo_name/image_name:optional_tag> .

Delete all images

    ➜ docker image prune -a

## Others

### Inspecting an Image

Inspect an image

    ➜ docker inspect <images>

Show image layers

    ➜ docker image history <image>

Change tag for the image to push on dockerhub

    ➜ docker tag getting-started <dockerhub_user>/getting-started

Push to the repository

    ➜ docker push <repository_path>

### Digests

Digest is unuque identifier of an image.

Show digests

    ➜ docker images --digests

Show digests for an image

    ➜ docker images --digests ubuntu

Pull an images using digest

    ➜ docker pull ubuntu@sha256:27cb6e6ccef575a4698b66f5de06c7ecd61589132d5a91d098f7f3f9285415a9

### Change Image

Change tag for the image to push on dockerhub

    ➜ docker tag getting-started <dockerhub_user>/getting-started

Push to the repository

    ➜ docker push <repository_path>

