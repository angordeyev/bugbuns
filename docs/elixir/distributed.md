# Distributed

## Named Node

### Using Shortname

Run a named node

    ➜ iex --sname a
    iex(a@computer-name)1>

Define module

    iex> defmodule M, do: def f, do: :shared

Connect to the named node

    ➜ iex --sname b --remsh a
    iex(a@angarch)1>

Use the code from node "a"

    iex> M.f
    :shared

### Using Fullname

The following variants allows to connect from another node

    ➜ iex --name a@localhost
    iex(a@localhost)1>

    ➜ iex --name a@127.0.0.1
    iex(a@127.0.0.1)1>

    ➜ iex --name a@some.local.ip.address
    iex(a@some.local.ip.address)1>

    ➜ iex --name a@computer-name
    iex(a@computername)1>

The following variants starts, but does not allow to connect from another node

    ➜ iex --name a@nonexisting-host-name
    iex(a@nonexisting-host-name)1>

    ➜ iex --name a@non.existing.ip.address
    iex(a@non.existing.ip.address)1>

Remsh requies remsh node to use fully qualified name as well

    ➜ iex --name a@127.0.0.1
    ➜ iex --name b@127.0.0.1 --remsh a@127.0.0.1
