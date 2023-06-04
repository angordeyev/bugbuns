# case

## Example

```elixir
# matches has order

o = 1

m =
  case o do
    _some -> :some
    1 -> :one
  end

IO.puts(m)

m =
  case o do
    1 -> :one
    _some -> :some
  end

IO.puts(m)

:ok
```
