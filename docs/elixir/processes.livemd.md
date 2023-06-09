# Processes

## Current Process Info

```elixir
self()
```

## Get Linked Processes

```elixir
Process.info(self(), :links)
```

## Spawning Processes

```elixir
# Using spawn

spawn(fn -> IO.puts("1") end)

a = fn -> IO.puts("2") end
spawn(a)

defmodule A do
  def a() do
    IO.puts("3")
    :ok
  end
end

spawn(&A.a/0)
```

```elixir
# Start task
task = Task.start(fn -> "hello" end)
IO.inspect(task, label: "Task")

# Async task
async_task = Task.async(fn -> "async" end)
IO.inspect(async_task, label: "Async task")

IO.puts("Hello " <> Task.await(async_task))

:ok
```

<!-- livebook:{"disable_formatting":true} -->

```elixir
# Links the process manually

pid = spawn(fn -> receive do :ok -> :ok end end)

{:links, pids} = Process.info(self(), :links)

IO.inspect(Enum.member?(pids, pid)) # false

# Links process
Process.link(pid)
{:links, pids} = Process.info(self(), :links)

IO.inspect(Enum.member?(pids, pid)) # true

:ok
```

<!-- livebook:{"disable_formatting":true} -->

```elixir
# Send and receive a message

pid =
  spawn(fn ->
    receive do
      message -> IO.puts(message)
    end
  end)

send(pid, "Hello spawned")
:ok
```

```elixir
# Receive loop

defmodule MainModule do
  def loop() do
    receive do
      message -> IO.puts(message)
    end

    loop()
  end
end

pid = spawn(&MainModule.loop/0)

send(pid, "Hello loop 1")
send(pid, "Hello loop 2")

:ok
```
