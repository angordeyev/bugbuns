# Operators

## Basic Operators

## Relax Operators Usage

```elixir
m = %{a: 1}
IO.inspect(nil, label: "m[:b]")
# return :alternative if the firest part is nil
m[:b] || :alternative
```
