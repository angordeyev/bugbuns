# gpg

## Create a Key

```shell
export KEY_NAME="<key name>"
export KEY_COMMENT="<key commend>"

gpg --batch --full-generate-key <<EOF
%no-protection
Key-Type: 1
Key-Length: 4096
Subkey-Type: 1
Subkey-Length: 4096
Expire-Date: 0
Name-Comment: ${KEY_COMMENT}
Name-Real: ${KEY_NAME}
EOF
```

## List Keys

```shell
gpg --list-keys
```
