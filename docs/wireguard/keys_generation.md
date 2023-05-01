# Keys Generation

## Generate a Private Key and Save to File

```shell
wg genkey > /etc/wireguard/private.key
```

## Generate Public and Private Keys

```shell
private_key=$(wg genkey)
public_key=$(echo ${private_key} | wg pubkey)
echo "Private key: ${private_key}"
echo "Public key:  ${public_key}"
```
```output
Private key: long_private_key
Public key:  long_public_key
```
