## Cookbook

## mix.exs Versions

If you upgraded to the next version, then reverted and get errors, `git checkout mix.lock` and rebuild, it may help. Checkout will revert previosuly locked versions of components.

## inets

In case of inets error after Phoenix release

```output
(MatchError) no match of right hand side value: {:error, {:inets, {'no such file or directory', 'inets.app'}}}
```

Add `inets` to `extra_applications` in `mix.exs`

```elixir
def application do
  [
    ...
    extra_applications: [:logger, :runtime_tools, :inets]
    ...
  ]
end
```

## Conditional Compilation

```elixir
defmodule HelloConditional do
  if Mix.env() in [:dev, :test] do
    def hello_dev do
      "hello dev"
    end
  end

  if Mix.env() == :prod do
    def hello_dev do
      "hello prod"
    end
  end
end
```

```shell
MIX_ENV=dev iex -S mix
```

```elixir
iex> HelloConditional.hello_dev()
```
```output
"hello_dev"
```

```elixir
iex> HelloConditional.hello_prod()
```
```output
(UndefinedFunctionError) function HelloConditional.hello_prod/0 is undefined
```

```shell
MIX_ENV=prod iex -S mix
```

```elixir
iex> HelloConditional.hello_prod()
```
```output
"hello_prod"
```

```elixir
iex> HelloConditional.hello_dev()
```
```output
(UndefinedFunctionError) function HelloConditional.hello_dev/0 is undefined
```

## Compile-time Code

```elixir
# HelloCompileTime.ex
IO.puts("out of module")
defmodule HelloCompileTime do
  IO.puts("in module")
end
```

```shell
mix compile
```
```output
out of module
in module
```

```elixir
iex -S mix # no messages
```

