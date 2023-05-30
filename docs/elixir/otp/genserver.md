# GenServer Cheat Sheet

```elixir
defmodule Counter do
  use GenStage

  def start_link(callback) do
    GenServer.start_link(__MODULE__, {0, callback })
  end

  def init(state) do
    {:ok, state}
  end

  def increment(pid) do
    GenServer.call(pid, :increment)
  end

  def handle_call(:increment, from, {counter, callback}) do
    {:reply, "current: #{counter+1}", {counter + 1, callback} }
  end

  def count(pid) do
    GenServer.cast(pid, :count)
  end

  def handle_cast(:count, state) do
    spawn(Counter, :count_cycle, [state])
    {:noreply, state}
  end

  def count_cycle({counter, callback}) do
    callback.(counter)
    :timer.sleep(1000)
    count_cycle({counter + 1, callback})
  end

  def printing(pid) do
    GenServer.cast(pid, :printing)
  end

  def handle_cast(:printing, c) do
    putter(1)
    {:noreply}
  end

  def putter(i) do
    IO.puts i
    :timer.sleep(2000)
    putter(i)
  end

  def cb(callback) do
    callback.()
  end
end
```
