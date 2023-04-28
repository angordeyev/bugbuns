# Logging

## Seeing Logs

Run the container in the first terminal window

    docker run -it ubuntu

Put a command in the running container

    echo "Hello Logs"

See logs in a second termainal window

    docker logs <container>

## Logging Driver

Container log files

    /var/lib/docker/containers/<container_id>/<container_id>-json.log

Get Docker logging driver

    docker info --format '{{.LoggingDriver}}'
    docker info | grep -i "logging driver" # the same

Get a running container logging driver

    docker inspect -f '{{.HostConfig.LogConfig.Type}}' <CONTAINER>

Run a container and change logging driver

    docker run -it --log-driver none ubuntu

## Resources

[Run Filebeat on Dockeredit](https://www.elastic.co/guide/en/beats/filebeat/current/running-on-docker.html)
[Ship logs with Filebeat](https://docs.logz.io/shipping/log-sources/filebeat.html)
[Debug Fly](https://debug.fly.dev/)
