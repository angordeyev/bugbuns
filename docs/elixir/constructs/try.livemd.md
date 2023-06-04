# Try

## Basics

[try/rescue vs try/catch](https://stackoverflow.com/questions/40280887/elixir-try-catch-vs-try-rescue#:~:text=Both%20try%2Frescue%20and%20try,chapter%20in%20the%20introduction%20guide.&text=On%20the%20other%20hand%2C,by%20using%20throw%20and%20catch%20)

> Mainly, you should use throw for control-flow and reserve raise for errors, which happens on > developer mistakes or under exceptional circumstances.

```elixir
try do
  raise "error"
rescue
  e -> IO.inspect(e)
end
```

```elixir
try do
  raise "error"
catch
  e -> IO.inspect(e)
end
```

```elixir
try do
  throw("error")
catch
  e -> IO.inspect(e)
end
```

```elixir
try do
  throw("error")
rescue
  e -> IO.inspect(e)
end
```

```elixir
try do
  Map.fetch!(%{}, 1)
rescue
  KeyError -> :rescued
end
```

```elixir
try do
  1 / 0
rescue
  ArithmeticError -> :rescued
end
```
