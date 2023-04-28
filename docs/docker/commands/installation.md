# Installation

## Run without sudo

### Variant 1

Create group docker
    
    sudo groupadd docker

Add the user to the group

    sudo usermod -aG docker $USER

Relogin and test you can run docker without sudo

    docker run hello-world

### Variant 2

Edit docker service

    sudo nano /usr/lib/systemd/system/docker.service

Add

    [Service]
    ...
    ExecStartPre=/usr/bin/setfacl --modify user:<user>:rw /var/run/docker.sock
    ...
