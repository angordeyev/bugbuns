# Remote Shell

Connect to a release via remote shell.

## By Host Name (short name)

Run an application release node with environment variable:

```shell
SECRET_KEY_BASE=gK6UgeEmSWn3a9U46EMpwn07A8r4E8jFtZkPrxTyR+FFJP9VDgrARuW24uccyZge \
RELEASE_COOKIE=dQ04TFwEKVj+FKysuj4VA5vgg4myfU957nNXPYf5tvIEiD2VZeGMRB4nKB4bNzwr \
_build/prod/rel/phoenix_release/bin/server
```

Connect with the remote shell:

```shell
RELEASE_COOKIE=dQ04TFwEKVj+FKysuj4VA5vgg4myfU957nNXPYf5tvIEiD2VZeGMRB4nKB4bNzwr \
RELEASE_NODE=phoenix_release@<host> \
_build/prod/rel/phoenix_release/bin/phoenix_release remote
```

```shell
iex --sname remote \
  --cookie dQ04TFwEKVj+FKysuj4VA5vgg4myfU957nNXPYf5tvIEiD2VZeGMRB4nKB4bNzwr \
  --remsh phoenix_release@<host>
```

## By IP Address

Run an application release node with `RELEASE_COOKIE` environment variable:

```shell
SECRET_KEY_BASE=gK6UgeEmSWn3a9U46EMpwn07A8r4E8jFtZkPrxTyR+FFJP9VDgrARuW24uccyZge \
RELEASE_COOKIE=dQ04TFwEKVj+FKysuj4VA5vgg4myfU957nNXPYf5tvIEiD2VZeGMRB4nKB4bNzwr \
RELEASE_DISTRIBUTION=name
RELEASE_NODE=phoenix_release@<local_ip_address> \
_build/prod/rel/phoenix_release/bin/server
```

Connect with the remote shell from another node:

```shell
iex --name remote@localhost \
  --cookie dQ04TFwEKVj+FKysuj4VA5vgg4myfU957nNXPYf5tvIEiD2VZeGMRB4nKB4bNzwr \
  --remsh phoenix_release@<local_ip_address>
```
