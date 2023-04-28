# Network

List networks

    docker network ls

Create nework    

    docker network create <network_name>

Mapping TCP port

    docker run nginx -p 80:80

Mapping UDP port

    docker run <image> -p 12000:1200/udp
