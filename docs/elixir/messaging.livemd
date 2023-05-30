# Messaging

## Send and receive

```elixir
spawn(fn ->
  send(self(), "hello")

  receive do
    message ->
      IO.inspect(message)
  end

  send(self(), "bye")

  receive do
    message ->
      IO.inspect(message)
  end

  receive do
    # Nothing to receive
    message ->
      IO.inspect(message)
  end

  send(self(), "third")
end)

:ok
```

## No message

```elixir
spawn(fn ->
  IO.puts("first")

  receive do
    message -> IO.inspect(message)
  end

  IO.puts("next")
end)

:ok
```

## Send to another process

```elixir
pid =
  spawn(fn ->
    receive do
      message ->
        IO.inspect("received: #{message}")
    end

    IO.puts("after")
  end)

send(pid, "hi")
```
