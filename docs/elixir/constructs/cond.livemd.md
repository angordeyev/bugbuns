# cond

## Example

```elixir
cond do
  2 + 2 == 5 ->
    "This is never true"

  2 * 2 == 3 ->
    "Nor this"

  true ->
    "This"
end
```
