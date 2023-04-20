# ip

## ip rule

```cmd
ip rule
ip rule ls
```

```output
0:  from all lookup local
32766:  from all lookup main
32767:  from all lookup default
```

The first number is the priority (order), first numbers
are processed first like for an order numbers.

## ip link

> eth0: name of the interface
> BROADCAST: it’s a broadcast interface which means it has a valid broadcast address
> MULTICAST: it supports multicast
> UP: the interface has been enabled and running (drivers loaded and working)
> LOWER_UP: there is signal activity at the physical layer (a cable is plugged in)
> mtu 1500: the maximum  transfer unit is 1500
> qdisc pfifo_fast: used for packet queueing
> state UP: network interface is up
> group default: interface group
> qlen 1000: transmission queue length
> 
> -- [Linux for Network Engineers: Interface Information. NetBeez.](https://netbeez.net/blog/linux-interface-information/)

### set

    ip link set dev wg0 mtu 1420

## ip route

```cmd
ip route
ip route ls
```

Show all tables routes:

```cmd
ip route ls table all
```

[Network Schema. StackOveflow. Nassim.](https://serverfault.com/a/1058220/1003911)

## ip neigh

```cmd
ip neigh
ip neigh show
ip neigh list
ip neigh ls
```
