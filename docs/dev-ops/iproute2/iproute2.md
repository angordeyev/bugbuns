# iproute2

> | Commands           | Description                        |
> | ------------------ | ---------------------------------- |
> | ip link            | Link configuration                 |
> | ip addr            | Address configuration              |
> | ip route           | Routing tables                     |
> | ip neigh           | Neighbors                          |
> | ip tunnel          | Tunnels                            |
> | ip link set name   | Rename network interfaces          |
> | ip maddr           | Multicast                          |
> | bridge             | Handle bridge addresses and device |
> | ss                 | Show various networking statistics |
> | tc                 | Traffic control settings           |
>
> -- [iproute2. Wikipedia.](https://en.wikipedia.org/wiki/Iproute2)

## Install

On Ubuntu:

```cmd
apt-get install -y iproute2
```

## Getting Help

### Help

```cmd
ip help
ip link help
bridge help
bridge link help
ss --help
```

### Man Pages

```cmd
man ip
man ip address
man ip route
```

### More Readable Format

`c` - colored
`-- brief` - the shorted description in a table

```cmd
ip -c --brief link
ip -c --brief addr
```

### Short Form

```cmd
ip a
ip address

ip l
io link
```

## Protocols

Running command for IPv4:

```shell
ip -4 <command>
```

Running command for IPv6:

```shell
ip -6 <command>
```

## Frequently Used Commands

### ip addr

Show all network interfaces with addresses:

```cmd
ip addr
```

Show IPv4 and IPv6 addresses accordingly:

```cmd
ip -4 addr
```

```cmd
ip -6 addr
```

## Examples

same, shows network interfaces
    
    ip addr
    ip a

## Resources

[LARC (Linux Advanced Routing & Traffic Control HOWTO)](https://lartc.org/howto/)
[Task-centered iproute2 user guide. Daniil Baturin.](https://www.baturin.org/docs/iproute2/#overview-of-iproute2)
[Linux for Network Engineers: Interface Information](https://netbeez.net/blog/linux-interface-information/)
[What do the numbers mean in ip rule show command. StackOverflow](https://unix.stackexchange.com/questions/160115/what-do-the-numbers-mean-in-ip-rule-show-command)
