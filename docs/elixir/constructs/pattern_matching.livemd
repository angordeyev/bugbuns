# Pattern Matching

## Simple

```elixir

```

## Advanced

```elixir
defmodule Message do
  defstruct text: nil
end

# we can patten math struct to map
%{text: "hello"} = %Message{text: "hello"}

# reverse does not work
%Message{text: "hello"} = %{text: "hello"}
```

```elixir

```
