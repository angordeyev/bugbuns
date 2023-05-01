# Configuration

## CLI

### Show Configuration

Show the configuration for an interface in a text format:

    wg showconf wg0

Show the configuration for a key an interface:

    wg show wg0 listen-port
    wg show wg0 private-key
    wg show wg0 public-key
    wg show wg0 <peer_public_key>

### Change Configuration
    
#### Interface

Private key:

    bash -c "wg set wg0 private-key <(wg genkey)" # (bash process substitution syntax)

Listening port:

    wg set wg0 listen-port 51820

#### Peer

Set peer:

    wg set wg0 peer <peer_public_key>

Peer endpoint:

    wg set wg0 peer <peer_public_key> endpoint <peer_address:peer_port>

Peer allowed ips:

    wg set wg0 peer <peer_public_key> allowed-ips <peer_ip>/32

Delete peer:

    wg set wg0 peer <peer_public_key> remove
