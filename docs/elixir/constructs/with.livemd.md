# Constructions

## Matching

```elixir
o = {1, 1}

with {a, _b} <- o,
     {_, 1} <- o,
     {1, _} <- o do
  IO.puts(a)
end

:ok
```

## Not Matching

```elixir
o = {1, 1}

with {_a, _b} <- o,
     {2, _b} <- o do
  IO.puts("1")
end

:ok
```

## Not matching with Else

```elixir
o = {1, 1}

with {_a, _b} <- o,
     {2, _b} <- o do
  IO.puts("1")
else
  {1, 0} -> IO.puts("2")
  {1, 1} -> IO.puts("3")
end
```
