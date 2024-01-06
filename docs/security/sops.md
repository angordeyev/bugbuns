# sops

## Getting Started

Create gpg key:

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

List keys:
```shell
gpg --list-keys
```

Create a configuration:

```shell
cat << EOF > ~/.sops.yaml
creation_rules:
  - pgp: <public key>
EOF
```

## Resources

* [sops](https://github.com/getsops/sops)
* [A Comprehensive Guide to SOPS. GitGuardian.](https://blog.gitguardian.com/a-comprehensive-guide-to-sops/)
* [Mozilla Sops. Habr](https://habr.com/en/articles/590733/)
* [helm-secrets, sops, vault and envsubst. Habr.](https://habr.com/en/companies/ru_mts/articles/656351/)
