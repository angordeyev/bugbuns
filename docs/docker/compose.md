# Docker Compose

## Tasks

### Run from a File

```sh
docker compose -f <docker-compose-file.yml> up
```

### A Simple docker-compose file for a Dockerfile

Dockerfile

```docker
FROM debian:latest
```

docker-compose.yml

```yml
services:
  web:
    build: .
    volumes:
      - .:/app
```

Run a command in the image

```sh
docker compose run web ls
```

### Run a Single Service from docker-compose file

```sh
docker compose run -it <app>
```

### Health Check

[How to Successfully Implement A Healthcheck In Docker Compose. Rafia Zafar.](https://linuxhint.com/how-to-successfully-implement-healthcheck-in-docker-compose/)
