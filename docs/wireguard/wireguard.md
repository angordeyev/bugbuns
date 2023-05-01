# WireGuard

## Installing Wireguard

    sudo apt update && apt install wireguard

## Installing VPN server on Ubuntu 22

Upgrade OS

    sudo apt update && sudo apt upgrade

Enable forward and reload system configuration

    sudo sed -i 's/# *net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf
    sysctl -p

Install Wireguard

    apt install wireguard

## Configuration

Create server config

```bash
sudo tee /etc/wireguard/wg0.conf > /dev/null <<EOF
[Interface]
PrivateKey = $(wg genkey)
Address = 10.0.0.1/24
ListenPort = 8888
PostUp = iptables -A FORWARD -i %i -j ACCEPT
PostUp = iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT
PostDown = iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
EOF
```

Start as service

    ➜ sudo systemctl enable --now wg-quick@wg0

Check if the service is running

    ➜ sudo systemctl status wg-quick@wg0

### Generating client configs manually

Set client ip address and generate client keys

    ➜ CLIENT_IP_ADDRESS=10.0.0.2 &&
      CLIENT_PRIVATE_KEY=$(wg genkey) &&
      CLIENT_PUBLIC_KEY=$(echo ${CLIENT_PRIVATE_KEY} | wg pubkey)

Add client peer

```bash
# append to wg0.conf
sudo tee -a /etc/wireguard/wg0.conf > /dev/null <<EOF

[Peer]
PublicKey = ${CLIENT_PUBLIC_KEY}
AllowedIPs = ${CLIENT_IP_ADDRESS}/24
EOF
```

Restart the service

    ➜ sudo systemctl restart wg-quick@wg0
    
Check added peer

    ➜ sudo wg
    peer: <peer_public_key>
      allowed ips: 10.0.0.0/24

Get server keys and ip address

## Installing VPN client on Ubuntu 22

Upgrade OS

    ➜ sudo apt update && sudo apt upgrade

Enable forward and reload system configuration

    ➜ sudo sed -i 's/# *net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf
    ➜ sysctl -p

Install Wireguard

    ➜ apt install wireguard

## Adding peer

Generate client config on a server

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
Address = ${CLIENT_IP_ADDRESS}/24
ListenPort = 8888
DNS = 1.1.1.1,8.8.8.8

[Peer]
PublicKey = ${SERVER_PUBLIC_KEY}
Endpoint = ${SERVER_IP_ADDRESS}:8888
AllowedIPs = 0.0.0.0/0
EOF
```

Add the result /etc/wireguard/wg0.conf on the client machine

### Generating client configs

Add config templates

```bash
mkdir -p ./config_templates

sudo tee ./config_templates/client_config.tmpl > /dev/null <<'EOF'
[Interface]
PrivateKey = ${CLIENT_PRIVATE_KEY}
Address = ${CLIENT_IP_ADDRESS}/24
ListenPort = 8888
DNS = 1.1.1.1,8.8.8.8

[Peer]
PublicKey = ${SERVER_PUBLIC_KEY}
Endpoint = ${SERVER_IP_ADDRESS}:8888
AllowedIPs = 0.0.0.0/0
EOF

sudo tee ./config_templates/peer_config.tmpl > /dev/null <<'EOF'

[Peer]
PublicKey = ${CLIENT_PRIVATE_KEY}
AllowedIPs = ${CLIENT_IP_ADDRESS}/24
EOF
```

Save client config script

```bash
function server_public_key() {
  python3 << '  EOF' | sed -e 's/^  //';
  
  import configparser
  config = configparser.ConfigParser()
  config.read('/etc/wireguard/wg0.conf')
  print(config['Interface']['PrivateKey'])

  EOF
}

sudo tee generate_client_conf.sh > /dev/null <<'EOF'
sh -c "wg genkey | tee /etc/wireguard/client${1}_private.key | \
wg pubkey > /etc/wireguard/client${1}_public.key"

export SERVER_IP_ADDRESS=$(hostname --all-ip-addresses | awk '{print $1}')
export SERVER_PUBLIC_KEY=$(server_public_key)
export CLIENT_PRIVATE_KEY=$(cat /etc/wireguard/client${1}_private.key)
export CLIENT_IP_ADDRESS="10.0.0.$(($1 + 1))"
envsubst < ./config_templates/client_config.tmpl > "wg_client${1}.conf"
envsubst < ./config_templates/peer_config.tmpl >> "/etc/wireguard/wg0.conf"
rm "/etc/wireguard/client${1}_private.key"
rm "/etc/wireguard/client${1}_public.key"
EOF

chmod u+x generate_client_conf.sh
``` 

And execute script

    ./generate_client_conf.sh 1
    ...
    ./generate_client_conf.sh 5

#### TODO

Get server public key

```bash

python3 << EOF

import configparser
config = configparser.ConfigParser(strict=False)
config.read('/etc/wireguard/wg0.conf')
private_key = config['Interface']['PrivateKey']
print(private_key)

EOF
```

TODO python

```bash
sudo tee generate_client_conf.py > /dev/null <<'EOF'
import configparser
import textwrap

client_config_template = textwrap.dedent("""\
  [Interface]
  PrivateKey = {client_private_key}
  Address = {client_ip_address}/24
  ListenPort = 8888
  DNS = 1.1.1.1,8.8.8.8

  [Peer]
  PublicKey = {server_public_key}
  Endpoint = {server_ip_address}:8888
  AllowedIPs = 0.0.0.0/0
  """)

client_peer_config_temlate = textwrap.dedent("""\
  [Peer]
  PublicKey = {client_private_key}
  AllowedIPs = {client_ip_address}/24
""")

def server_public_key():
  config = configparser.ConfigParser()
  config.read('/etc/wireguard/wg0.conf')
  config['Interface']['PrivateKey']

export SERVER_IP_ADDRESS=$(hostname --all-ip-addresses | awk '{print $1}')
export SERVER_PUBLIC_KEY=$(server_public_key)
export CLIENT_PRIVATE_KEY=$(cat /etc/wireguard/client${1}_private.key)
export CLIENT_IP_ADDRESS="10.0.0.$(($1 + 1))"
EOF
```

## Installing client on Archlinux

### Installing

#### Existing config

Install Wireguard

    sudo pacman -S wireguard-tools

Copy config from server

    ssh root@178.62.226.219 "sudo cat /etc/wireguard/wg_client1.conf" | \
    sudo tee /etc/wireguard/wg0.conf > /dev/null

Start/stop

    wg-quick up wg0
    wg-quick down wg0

### New config

If config does not exist on a server follow this steps

Generate keys

    sudo sh -c 'wg genkey | tee /etc/wireguard/private.key | wg pubkey > /etc/wireguard/public.key'

Create config

    sudo nano /etc/wireguard/wg0.conf

Edit config

    [Interface]
    PrivateKey = <privatekey>
    Address = 10.0.0.2/24
    ListenPort = 8888

### Adding server peer

    [Peer]
    PublicKey = <server_public_key>
    Endpoint = 159.223.234.58:8888
    AllowedIPs = 0.0.0.0/0

## Install on iOS

### Generating QR code for the mobile app

    sudo apt install qrencode
    qrencode -t png -o client-qr.png -r wg-client.conf

Search WireGuard in App Store and install

## Diagnostic

[dnsleaktest](https://www.dnsleaktest.com/)
[whatismyipaddress](https://whatismyipaddress.com/)

Chech network interface

    ip a

Wireguard server status

    sudo systemctl status wg-quick@wg0

Check if ip forwarding is enabled

    sudo sysctl net.ipv4.ip_forward

Show iptables rules

    sudo iptables -S

Simple web server

    python3 -m http.server 8888

## Other

Forwarding

    iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

Delete interface

    sudo ip link delete wg0

## Resources

* [Installing](https://www.wireguard.com/install/)
* [Quick start](https://www.wireguard.com/quickstart/)
* [How would I pass the output of one command to multiple commands?](https://askubuntu.com/questions/833070/how-would-i-pass-the-output-of-one-command-to-multiple-commands)
* [FOUR WAYS TO VIEW WIREGUARD LOGS. Pro Custodibus.](https://www.procustodibus.com/blog/2021/03/wireguard-logs/)
