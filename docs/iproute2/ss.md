# ss

Show listening ports

```cmd
ss -tulp
```
Formatted

```cmd
ss -tulp | \
  tail -n +2 | \
  column -t -N Netid,State,Recv-Q,Send-Q,"Local Address:Port","Peer Address:Port",Process
```

# Getting help

    ➜ info ip
    ...
    ip - show / manipulate routing, network devices, interfaces and tunnels
    ...

    ➜ man ip address
    ...
    The ip address command displays addresses and their properties, 
    adds new addresses and deletes old ones.
    ...
