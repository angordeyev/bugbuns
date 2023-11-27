# Mimic

```elixir
Mix.install([
  {:mimic, "~> 1.7"}
])
```

## Code

```elixir
defmodule B do
  @callback f :: atom()
end

defmodule M do
  @behaviour B

  def f do
    :ok
  end
end

defmodule MStub do
  def f do
    :stub
  end
end
```

## Global Stub

```elixir
Mimic.copy(M)

ExUnit.start()

defmodule S do
  use ExUnit.Case, async: true

  use Mimic

  setup :set_mimic_global

  def set_global() do
    setup :set_mimic_global
  end

  def start() do
    stub_with(M, MStub)
  end
end

S.start()

defmodule UsingMimic do
  use ExUnit.Case, async: true
  use Mimic.DSL

  test "f 1" do
    stub_with(M, MStub)
  end

  test "f 2" do
    S.set_global()
    assert M.f() == :stub
    spawn(fn -> IO.inspect(M.f(), label: "M.f()") end)
  end
end

ExUnit.run()
```

## Partial Stub

```elixir
defmodule FG do
  def f do
    :f
  end

  def g do
    :g
  end
end

defmodule PartialStub do
  def f do
    :stub
  end
end

Mimic.copy(FG)
ExUnit.start()

defmodule FGTest do
  use ExUnit.Case, async: true
  use Mimic.DSL

  setup do
    stub_with(FG, PartialStub)
    :ok
  end

  test "f" do
    assert FG.f() == :f
  end

  test "g" do
    # assert FG.g == :g
  end
end

ExUnit.run()
```
