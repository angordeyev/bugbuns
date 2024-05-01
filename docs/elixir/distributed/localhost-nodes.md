# Localhost Nodes

## Using `resmsh`

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

Use the code from node `a`:

```elixir
iex> M.f
```

```output
:shared
```

## Using `Node.connect`

Run in different terminals:

```shell
iex --name a@127.0.0.1
```

```shell
iex --name b@127.0.0.1
```

On `a` node:

```elixir
defmodule A do
  def f do
    IO.puts "A"
  end
end
```

On `b` node:

```elixir
defmodule B do
  def f do
    IO.puts "B"
  end
end
```

On `a` node:

```elixir
Node.connect(:"b@127.0.0.1")
```

```elixir
Node.spawn(:"b@127.0.0.1", fn -> B.f() end)
```

```output
B
```

```elixir
Node.spawn(:"b@127.0.0.1", fn -> A.f() end)
```

```output
Process #PID<18931.131.0> on node :"b@127.0.0.1" raised an exception
** (UndefinedFunctionError) function A.f/0 is undefined or private
    A.f()
```

```elixir
Node.spawn(:"b@127.0.0.1", fn ->
  defmodule M do
    def f do
      IO.puts("M")
    end
  end

  M.f()
end)
```

```output
M
```
