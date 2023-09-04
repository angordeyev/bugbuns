# Performance

## Measure Execution time

Measure time in microseconds:

```elixir
:timer.tc(fn -> :timer.sleep(1000) end, [])
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

## Resources

[There is a huge problem with this sadly, the startup time of the BEAM is too much! ](https://news.ycombinator.com/item?id=25240905)
