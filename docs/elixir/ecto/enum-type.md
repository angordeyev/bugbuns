# Enum Type

```elixir
...
schema("users_actions") do
  ...
  field(:status, Ecto.Enum, values: [:not_synced, :in_sync, :synced])
  ...
end
...
```

## Resources

[Creating an Ecto Enum Type](https://dev.to/mnussbaumer/creating-an-ecto-enum-type-43dh)
