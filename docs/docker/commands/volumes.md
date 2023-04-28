# Volumes

List volumes

    docker volume ls

Run container with a mounted volume

    docker run -dp <host_port>:<container_port> -v <volume>:</mount/path> <image>

Inspect volume

    docker volume inspect <volume_name>

Remove volumes

    docker volume rm $(docker volume ls -qf dangling=true)
