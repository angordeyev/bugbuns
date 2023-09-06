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
```

### Filtered Send Messages

#### Exact Match

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

#### Pattern Match

```elixir
# Install `ex2ms` dependency:
Mix.install([:ex2ms])
import Ex2ms

:dbg.tracer()
:dbg.p(self(), :s)
filter = fun do [_receiver, {:some_msg_type, _}] = x -> x end
:dbg.tpe(:send, filter)
```

```elixir
pid = spawn(fn -> Process.sleep(:infinity) end)
send pid, {:another_msg_type, "hello"}
```

```output
{:another_msg_type, "hello"}
```

```elixir
send pid, {:some_msg_type, "hello"}
```

```output
(<0.114.0>) <0.174.0> ! {some_msg_type,<<"hello">>}
{:some_msg_type, "hello"}
```

#### Send to the Current Process

```elixir
# Install `ex2ms` dependency:
Mix.install([:ex2ms])
import Ex2ms

:dbg.tracer()
# Trace new processes
:dbg.p(:new, :s)
pid = self()
filter = fun do [pid, _] = x when pid == ^pid -> x end
:dbg.tpe(:send, filter)
```

```elixir
spawn fn -> send(pid, "hello") end
```

```output
#PID<0.174.0>
(<0.174.0>) <0.114.0> ! <<"hello">>
```

### Filtered Received Messages

#### Exact Match

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

#### Pattern Match

```elixir
# Install `ex2ms` dependency:
Mix.install([:ex2ms])
import Ex2ms

:dbg.tracer()
:dbg.p(self(), :r)
filter = fun do [_node, _sender, {:some_msg_type, _}] = x -> x end
:dbg.tpe(:receive, filter)
```

```elixir
pid = self()
spawn(fn -> send pid, {:another_msg_type, "hello"} end)
```

```output
#PID<0.178.0>

```

```elixir
pid = self()
spawn(fn -> send pid, {:some_msg_type, "hello"} end)
```

```output
#PID<0.179.0>
(<0.114.0>) << {some_msg_type,<<"hello">>}
```
