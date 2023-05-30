# Guards

## Basic pattern matching

```elixir
a = 1

case a do
  1 -> "11"
  2 -> "22"
end
```

```elixir
a = 2

case a do
  1 -> {1, 1}
  n when is_bitstring(n) -> {2, n}
  n when is_bitstring(n) -> {2, n}
  n when n in [3, 4] -> {2, n}
  n when is_integer(n) -> {3, n}
end
```

```elixir
a = 1

case a do
  Intege3r -> :ok
  _ -> :error
end
```

## Guards

```elixir
a = 1

case a do
  e in Integer -> "11"
  2 -> "22"
end
```
