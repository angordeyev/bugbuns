# dbg

## Trace Function Calls

With any arguments:

```elixir
:dbg.tracer()
:dbg.p(:all, :c)
:dbg.tpl(Enum, :count, :x)
```

```elixir
Enum.count([1,2,3])
```

```output
(<0.114.0>) call 'Elixir.Enum':count([1,2,3])
(<0.114.0>) returned from 'Elixir.Enum':count/1 -> 3
```

With matching arguments:

```elixir
:dbg.tracer()
:dbg.p(:all, :c)
filter = :dbg.fun2ms(fn [s] when s == [1,2,3] -> :return_trace end)
:dbg.tpl(Enum, :count, filter)
```

```elixir
Enum.count([1,2])
```

```output
2
```

```elixir
Enum.count([1,2,3])
```

```output
(<0.114.0>) call 'Elixir.Enum':count([1,2,3])
3
```

## Trace Messages


### All Messages

```elixir
:dbg.tracer()
:dbg.p(self(), :m)
:dbg.tpe(:send, :x)
```

### Filtered Send Messages

```elixir
:dbg.tracer()
:dbg.p(self(), :s)
filter = :dbg.fun2ms(fn [_receiver, msg] when msg == "hello" -> :return_trace end)
:dbg.tpe(:send, filter)
```

```elixir
send self(), "hi"
```

```output
```

```elixir
send self(), "hello"
```

```output
(<0.114.0>) <0.114.0> ! <<"hello">>
```

### Filtered Received Messages

```elixir
:dbg.tracer()
:dbg.p(self(), :r)
filter = :dbg.fun2ms(fn [_node, _sender, msg] when msg == "hello" -> :return_trace end)
:dbg.tpe(:receive, filter)
```

```elixir
send self(), "hi"
```

```output
```

```elixir
send self(), "hello"
```

```output
(<0.114.0>) << <<"hello">>
```
