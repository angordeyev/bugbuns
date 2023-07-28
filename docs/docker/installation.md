# Installation

## Run without sudo

Edit docker service

    sudo nano /usr/lib/systemd/system/docker.service

Add

    [Service]
    ...
    ExecStartPre=/usr/bin/setfacl --modify user:<user>:rw /var/run/docker.sock
    ...
