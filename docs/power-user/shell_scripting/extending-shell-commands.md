# Extending Shell Commands

## Ways to Extend

### Aliases with Dashes

```shell
alias vpn-on="sudo wg-quick up wg0"
alias vpn-off="sudo wg-quick down wg0"
```

### Function

```shell
function vpn() {
  case $1 in
    ""|--help)
      echo "Commands:"
      echo "  on      Turn on VPN"
      echo "  off     Turn off VPN"
      ;;
    on)
      sudo wg-quick up wg0
      ;;
    off)
      sudo wg-quick down wg0
      ;;
    *)
      echo "vpn: '${1}' is not a vpn command. See 'vpn --help.'"
      ;;
  esac
}
```

## Adding New Commands

Git supports aliases configuration.

## Wrapping

### With Same Name

```shell
function docker() {
  /usr/bin/docker $@
}
```

### With Different Name

Wrapping `ls`:

```shell
function lsex() {
  ls $@
}
```

Test:

```shell
lsex -l --author
```

## Resources

* [amplify. Engin Polat](https://github.com/microsoft/amplify)
