# Mimics And Mock comparation

```elixir
Mix.install([
  {:mimic, "~> 1.7"},
  {:mock, "~> 0.3.7"}
])
```

## Code

```elixir
defmodule Calculator do
  def add(a, b) do
    a + b
  end

  def multiply(a, b) do
    a * b
  end
end
```

## Test

```elixir
ExUnit.start(auto_run: false)

defmodule UsingMimic do
  use ExUnit.Case, async: true
  use Mimic.DSL

  test "add" do
    expect(Calculator.add(x, y), do: x + y)
    assert Calculator.add(2, 3) == 5
  end
end

defmodule UsingMock do
  use ExUnit.Case
  import Mock

  test "add" do
    with_mock Calculator, add: fn x, y -> x + y end do
      assert Calculator.add(2, 3) == 5
    end
  end
end

Mimic.copy(Calculator)
ExUnit.run()
```
