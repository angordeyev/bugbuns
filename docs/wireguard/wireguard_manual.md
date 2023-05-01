# WireGuard Manual VPN Setup

## Installing VPN Server on Ubuntu 22

Upgrade OS and install WireGuard

    sudo apt update && sudo apt upgrade &&
    sudo apt install wireguard

Enable forward and reload system configuration

    sudo sed -i 's/# *net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf
    sudo sysctl -p

Create server config

```bash
sudo tee /etc/wireguard/wg0.conf > /dev/null <<EOF
[Interface]
PrivateKey = $(wg genkey)
Address = 10.0.0.1/32
ListenPort = 8888
PostUp = iptables -A FORWARD -i %i -j ACCEPT
PostUp = iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT
PostDown = iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
EOF
```

Start as service

    sudo systemctl enable --now wg-quick@wg0

Check if the service is running

    sudo systemctl status wg-quick@wg0

## Adding Client Peer with Ubuntu 22 Client

### On Server

Set client ip address and generate client keys

    CLIENT_IP_ADDRESS=10.0.0.3 &&
    CLIENT_PRIVATE_KEY=$(wg genkey) &&
    CLIENT_PUBLIC_KEY=$(echo ${CLIENT_PRIVATE_KEY} | wg pubkey)

Add client peer

```bash
sudo tee -a /etc/wireguard/wg0.conf > /dev/null <<EOF
[Peer]
PublicKey = ${CLIENT_PUBLIC_KEY}
AllowedIPs = ${CLIENT_IP_ADDRESS}/32
EOF
```

Generate a client config on a server

```bash
SERVER_PRIVATE_KEY=$(python3 << EOF
import configparser
config = configparser.ConfigParser(strict=False)
config.read('/etc/wireguard/wg0.conf')
private_key = config['Interface']['PrivateKey']
print(private_key)
EOF
)

SERVER_PUBLIC_KEY=$(echo ${SERVER_PRIVATE_KEY} | wg pubkey)
SERVER_IP_ADDRESS=$(hostname --all-ip-addresses | awk '{print $1}')

cat << EOF
[Interface]
PrivateKey = ${CLIENT_PRIVATE_KEY}
Address = ${CLIENT_IP_ADDRESS}/32
ListenPort = 8888
DNS = 1.1.1.1,8.8.8.8

[Peer]
PublicKey = ${SERVER_PUBLIC_KEY}
Endpoint = ${SERVER_IP_ADDRESS}:8888
AllowedIPs = 0.0.0.0/0
EOF
```

Restart the service

    sudo systemctl restart wg-quick@wg0

### On Client

Install WireGuard and resolveconf 

    sudo apt install wireguard resolvconf

Copy the client config generated on the server to 

    nano /etc/wireguard/wg0.conf

Start client

    sudo wg-quick up wg0
    
Try to ping server

    ping 10.0.0.1

Check addeded peer, see `handshake` and `transfer`

    sudo wg
    interface: wg0
      ...
    peer: ...
      ...
      latest handshake: 5 seconds ago
      transfer: 256 B received, 256 B sent
