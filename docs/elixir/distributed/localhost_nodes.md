# Localhost Nodes

Run a named node:

```shell
iex --sname a
```

```output
iex(a@computer-name)1>
```

Define a module:

```elixir
iex> defmodule M, do: def f, do: :shared
```

Connect to the named node:

```shell
iex --sname b --remsh a
```

```output
iex(a@angarch)1>
```

Use the code from node "a":

```elixir
iex> M.f
```

```output
:shared
```
