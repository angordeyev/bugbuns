# Test Environment

## Simple

    docker run -it ubuntu

## Experiments

[How do I run a docker instance from a Dockerfile?](https://stackoverflow.com/questions/36075525/how-do-i-run-a-docker-instance-from-a-dockerfile)

    docker build --no-cache . | \
    grep "Successfully built" | \
    sed 's/Successfully built //g' | \
    xargs -I{} docker run {}


Dockerfile

    FROM ubuntu:latest
    
    RUN apt-get update && apt-get install -y curl

## Run

```
docker build - << EOF
FROM ubuntu:latest
RUN apt-get update && apt-get install -y ubuntu-server
EOF
```
