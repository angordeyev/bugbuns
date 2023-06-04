# Working with Enum

## define

<!-- livebook:{"reevaluate_automatically":true} -->

```elixir
list = [1, 2, 3]
```

## each

<!-- livebook:{"reevaluate_automatically":true} -->

```elixir
Enum.each(list, fn x -> IO.puts(x) end)
```

## map

```elixir
Enum.map(list, fn x -> x * 2 end)
```

## reduce, foldl, foldr

<!-- livebook:{"reevaluate_automatically":true} -->

```elixir
list
|> Enum.reduce(fn x, acc -> "#{acc} #{x}" end)
|> IO.inspect()

list
|> Enum.reduce(0, fn x, acc -> "#{acc} #{x}" end)
|> IO.inspect()

# foldl and foldr are implemented for List, List.foldl is the same as Enum.reduce

list
|> List.foldl(0, fn x, acc -> "#{acc} #{x}" end)
|> IO.inspect()

list
|> List.foldr(0, fn x, acc -> "#{acc} #{x}" end)
|> IO.inspect()

:ok
```

## Into

```elixir
IO.inspect(Enum.into([1, 2, 3], []))

IO.inspect(Enum.into(%{c: 3}, %{a: 1, b: 2}))
:ok
```

## Map

```elixir
# Map is Enumerable and returns keyword list.
IO.inspect(Enum.map(%{a: 1, b: 2}, & &1))

IO.inspect(Enum.into(%{c: 3}, %{a: 1, b: 2}))

IO.inspect(Enum.into(%{a: 5}, %{a: 1, b: 2}))

:ok
```
