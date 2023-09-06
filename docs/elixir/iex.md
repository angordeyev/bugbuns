# IEx

## Tips and Tricks

Paste multiline


```elixir
(
  IO.puts("hi")
  IO.puts("middle")
  IO.puts("bye")
)
```

Configure colors

```elixir
IEx.configure(
  colors:
      [eval_error: [IO.ANSI.color(5,1,1)],
       stack_info: [IO.ANSI.color(1,2,1)] ]
)
```

## Import Dependencies

```elixir
Mix.install([:table_rex])

rows = [
  ["11", "12", "13"],
  ["21", "22", "23"],
  ["31", "32", "33"]
]

IO.puts(TableRex.quick_render!(rows))
```

## Resources

[Customizing Elixirs IEx](http://samuelmullen.com/articles/customizing_elixirs_iex/)
[Usefull IEx tips](https://itnext.io/a-collection-of-tips-for-elixirs-interactive-shell-iex-bff5e177405b)
[IEx Official Docs](https://hexdocs.pm/iex/IEx.html)
