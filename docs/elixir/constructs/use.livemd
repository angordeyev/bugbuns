# Use

```elixir
ExUnit.start()
```

## Use

`use` is macro and can be called like like `use(Module, opts)` or `use Module, opts`
It can be used inside a module only.

```elixir
defmodule SomeModule do
  use ExUnit.Case

  # assert can be used now
  assert true
end
```

## Without parameters

```elixir
defmodule Mathematical do
  defmacro __using__(_opts) do
    quote do
      import :math

      def some_function do
        "some result"
      end
    end
  end
end

defmodule Calculations do
  use Mathematical

  def calculate() do
    # can use pow without :math module name
    IO.inspect(pow(2, 3))
    IO.inspect(some_function())
  end
end

Calculations.calculate()
```

## With parameters

```elixir
defmodule Mathematical do
  defmacro __using__(which) do
    # aplly: to call function dynamically by name
    apply(__MODULE__, which, [])
  end

  def some do
    # returns the code injected in a module
    quote do
      import :math

      def some_function() do
        "some result"
      end
    end
  end
end

defmodule Calculations do
  # use(module, opts)
  use Mathematical, :some

  def calculate() do
    # can use pow without :math module name
    IO.inspect(pow(2, 3))
    IO.inspect(some_function())
  end
end

Calculations.calculate()
```
