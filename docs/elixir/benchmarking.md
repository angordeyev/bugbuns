## Benchmarking

### Measure function execution time

    iex> :timer.tc(fn ->
      IO.puts("hello benchmark")
    end)

    hello benchmark
    {92, :ok}

### Measure file script execution time

    ➜ echo 'IO.puts("hi")' > script.exs

    iex> :timer.tc(fn ->
      Code.eval_file "script.exs"
    end)

    {419, {:ok, []}} # microseconds
