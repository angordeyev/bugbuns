# Module

## Additional Code

```elixir
defmodule M do
  # Compile time
  Application.put_env(:iex, :some, "value")

  def get_some() do
    Application.get_env(:iex, :some)
  end
end
```

## @on_load

```elixir
defmodule M do
  @on_load :on_load
  def on_load do
    Application.put_env(:iex, :some, "value")
  end

  def get_some do
    Application.get_env(:iex, :some)
  end
end
```


