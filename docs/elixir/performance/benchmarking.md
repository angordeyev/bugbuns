# Benchmarking

## With Hyperfine

```shell
hyperfine --warmup 2 -S none --export-markdown results.md -- 'elixir -e \'System.halt(0)\'' 'elixir -e \'IO.puts("Hello world")\''
```

## Measure Function Execution Time

```elixir
iex> :timer.tc(fn ->
  IO.puts("hello benchmark")
end)
```
```output
hello benchmark
{92, :ok}
```

## Measure File Script Execution Time

```shell
echo 'IO.puts("hi")' > script.exs
```

```elixir
iex> :timer.tc(fn ->
  Code.eval_file "script.exs"
end)
```
```output
{419, {:ok, []}} # microseconds
```

