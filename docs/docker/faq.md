# Questions

[Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy)

## Taking Latest Docker Image

Go to https://hub.docker.com/_/<repository-name>/tags

## Differeneces between ADD and COPY

ADD is more morefull and supports URLs and extracting tar

[Difference between the COPY and ADD commands in a Dockerfile](https://www.geeksforgeeks.org/difference-between-the-copy-and-add-commands-in-a-dockerfile/)

COPY is preffered according to [the best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy)

## ARGS vs ENV

From Dockerfile reference:

The ARG instruction defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag.

The ENV instruction sets the environment variable <key> to the value <value>.
The environment variables set using ENV will persist when a container is run from the resulting image.

[Docker ARG, ENV and .env - a Complete Guide](https://vsupalov.com/docker-arg-env-variable-guide/)

## Docker Registry API

[Docker Registry HTTP API V2](https://docs.docker.com/registry/spec/api/#listing-image-tags)
