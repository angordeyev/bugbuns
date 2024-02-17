# Local Network Nodes

Prerequisites:

Create two Debian hosts named node1 and node2 connected with a local network.

Install Erlang and Elixir on the nodes:

```shell
sudo apt-get -y install erlang
sudo apt-get -y install elixir
```

## Using Host Names

### node1

Add to hosts file:

```title="/etc/hosts"
<node2_ip_address> node2
```

```shell
iex --sname 1 --cookie <cookie>
```

```elixir
iex> defmodule M, do: def f, do: :shared
```

### node2

Add to hosts file:

```title="/etc/hosts"
<node1_ip_address> node1
```

```shell
iex --sname 2 --remsh 1@node1 --cookie <cookie>
```

```elixir
iex> M.f()
```

```output
:shared
```

## Using IP Addresses

Create two Debian hosts namade node1 and node2 connected with a local network.

Install Erlang and Elixir on the nodes:

```shell
sudo apt-get -y install erlang
sudo apt-get -y install elixir
```

### node1

```shell
iex --name node1@<node1_local_ip_address> --cookie <cookie>
```

```elixir
iex> defmodule M, do: def f, do: :shared
```

### node2

```shell
iex --name node2@<node2_local_ip_address> --remsh <node1_local_ip_address> --cookie <cookie>
```

```elixir
iex> M.f()
```

```output
:shared
```
