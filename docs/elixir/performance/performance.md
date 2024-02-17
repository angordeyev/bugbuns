# Performance

## Measure Execution time

Measure time in microseconds:

```elixir
:timer.tc(fn ->
  :timer.sleep(1000)
end)
```

```output
{1000801, :ok}
```

## Faster boot time

```cmd
time /usr/local/lib/erlang23/bin/erl \
  -eval 'io:format("hi~n"), halt(0, [{flush, false}])' \
  -noshell -start_epmd false -boot no_dot_erlang hi
```

## Message Passing

Without a process:

```elixir
v = 1
:timer.tc(fn ->

  1..1000000 |> Enum.reduce(fn _x, acc -> acc + v end)

  end,[]
)
```

```output
{1 256 803, 1000000}
```

With a process:

```elixir
{:ok, pid} = Agent.start_link(fn -> 1 end)

:timer.tc(fn ->

  1..1000000 |> Enum.reduce(fn _x, acc -> acc + Agent.get(pid, & &1) end)

  end,[]
)
```

```output
{22 791 091, 1000000}
```

## Resources

* [Why is erlc so quick to start?](https://erlang.org/pipermail/erlang-questions/2015-January/082392.html)
* [There is a huge problem with this sadly, the startup time of the BEAM is too much! ](https://news.ycombinator.com/item?id=25240905)
* [How to minimise BEAM startup time? Elixir Forum.](https://elixirforum.com/t/how-to-minimise-beam-startup-time/31913/3)
