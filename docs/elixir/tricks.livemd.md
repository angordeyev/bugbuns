# Untitled notebook

## Use function like variable

```elixir
defmodule Config do
  def conf() do
    %{
      a: 1,
      b: 2
    }
  end
end

# skip braces
Config.conf()[:a]
```
