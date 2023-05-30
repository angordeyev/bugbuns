# Streams

## Experiments

```elixir
# Streams without state (ideponent, a same operation on stream the same result)

range = 1..10
IO.inspect(Enum.take(range, 5), label: "range")
IO.inspect(Enum.take(range, 5), label: "range")

# Build simple repeat stream
Stream.repeatedly(fn -> 1 end)
|> Enum.take(5)
|> IO.inspect(label: "repeat")

doubling_series = Stream.iterate(1, fn number -> number * 2 end)
IO.inspect(Enum.take(doubling_series, 5), label: "doubling")

# Streams with state

# Resource stream is the most flexible one
resource_stream = Stream.resource(fn -> 1 end, fn {x, 5, true} -> {[x], {x, 1, true}} end, fn _x  -> nil end)
Enum.take(resource_stream, 3)

defmodule Resource do

end

# String stream
{:ok, pid} = StringIO.open("line1\nline2\n")
IO.inspect(IO.read(pid, :line))
IO.inspect(IO.read(pid, :line))

:ok
```

## Resources

[Having fun with Elixit streams](https://medium.com/@leo_hetsch/having-fun-with-elixir-streams-537d687366ab)

[Learn With Me: Elixir - Streams ](https://inquisitivedeveloper.com/lwm-elixir-43/)
