# Agent

## Global Variable Agent

Defining:

```elixir
defmodule Variable do
  use Agent

  def init(value) do
    {:ok, pid} = Agent.start_link(fn -> value end)
    pid
  end

  def get(pid) do
    Agent.get(pid, & &1)
  end

  def set(pid, value) do
    Agent.update(pid, fn _state -> value end)
  end
end
```

Using:

```elixir
p = Variable.init(5)
Variable.get(p)
```

```output
5
```

```elixir
Variable.set(p, 6)
Variable.get(p)
```

```output
6
```


