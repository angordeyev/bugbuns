# meck

```elixir
Mix.install([
  {:meck, "~> 0.9.2"}
])
```

## Mock a Function

Define a module:

```elixir
defmodule MF do
  def f do
    :ok
  end
end
```

Mock the function `f`

```elixir
:meck.expect(MF, :f, fn -> :error end)
```

Use the function:

```elixir
IO.inspect(MF.f())
spawn(fn -> IO.inspect(M.f()) end)
```

## Mock a Module

```elixir
defmodule MFG do
  def f do
    :ok
  end

  def g do
    :ok
  end
end
```
