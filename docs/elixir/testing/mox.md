# Mox

Install meck:

```elixir
Mix.install [:mox]
```

Import `Mox`:

```elixir
import Mox
```

Define a behaviour:

```elixir
defmodule B do
  @callback f :: atom()
end
```

Define a module:

```elixir
defmodule M do
  @behaviour B

  def f do
    :ok
  end
end
```

Define a mock:

```elixir
Mox.defmock(Mock, for: B)
|> expect(:f, fn  -> :error end)
```

Access a mock:

```elixir
Mock.f()
spawn(fn -> IO.inspect(Mock.f()) end)
```

Stub:

```elixir
stub(M, :f, fn  -> :error end)
```

# TODO
<!-- ```elixir
stub_with(Mock, M)
``` -->
[]
