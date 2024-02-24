# Remote Shell

Connect to a release via remote shell.

Use `mix phx.gen.secret` to generate SECRET_KEY_BASE and RELEASE_COOKIE.

## By Host Name (short name)

Run an application release node with environment variable:

```shell
SECRET_KEY_BASE=<SECRET_KEY_BASE> \
RELEASE_COOKIE=<RELEASE_COOKIE> \
_build/prod/rel/phoenix_release/bin/server
```

Connect with the remote shell:

```shell
RELEASE_COOKIE=<RELEASE_COOKIE> \
RELEASE_NODE=<node_short_name>@<host> \
_build/prod/rel/phoenix_release/bin/phoenix_release remote
```

```shell
iex --sname remote \
  --cookie <COOKIE> \
  --remsh <node_short_name>@<host>
```

## By IP Address

Run an application release node with `RELEASE_COOKIE` environment variable:

```shell
SECRET_KEY_BASE=<SECRET_KEY_BASE>
RELEASE_COOKIE=<RELEASE_COOKIE> \
RELEASE_DISTRIBUTION=name \
RELEASE_NODE=<node_name>@<local_network_ip_address> \
_build/prod/rel/phoenix_release/bin/server
```

Connect with the remote shell from another node:

```shell
iex --name remote@localhost \
  --cookie <COOKIE> \
  --remsh <node_name>@<local_network_ip_address>
```
