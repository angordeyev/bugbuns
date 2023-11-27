# Metaprogramming

```elixir
ExUnit.start()
```

## Quote

Quote returns code in AST format

```elixir
quote do: 1 + 1
```

```elixir
quote do: 1 + 2 + 3
```

```elixir
defmodule SomeTest do
  use ExUnit.Case

  test "check if assert works" do
    assert 1 == 1
  end
end
```

```elixir
defmodule ArgCode do
  defmacro get_arg(arg) do
    IO.inspect(arg)
    :ok
  end
end
```

```elixir
defmodule CalcutorTest do
  use ExUnit.Case, async: false

  test "2 plus 3 is 5" do
    assert Calculator.add(2, 3) == 5
    assert 1 == 2
  end
end
```

```elixir
defmodule ArgsCode do
  defmacro get_arg(arg) do
    IO.inspect(arg)
    :ok
  end

  defmacro get_args(arg1, arg2) do
    IO.inspect(arg1, label: "arg1")
    IO.inspect(arg2, label: "arg2")
    :ok
  end

  defmacro test_args() do
    quote do: 1 + 1
  end

  def get_ast(module, function_string) do
    apply(module, :"MACRO-#{function_string}", [__ENV__])
  end
end

defmodule Work do
  require ArgsCode

  def do_work() do
    # https://elixirforum.com/t/how-to-get-the-ast-that-would-be-generated-by-the-given-macro/41323
    # https://sgeos.github.io/elixir/metaprogramming/ast/2016/01/31/elixir-execute-ast.html

    ArgsCode.get_ast(ArgsCode, "test_args")

    code = quote do: 1 + 2 + 3
    Code.eval_quoted(code)
  end
end

Work.do_work()
```

## Unquote

`unquote` subsitutes the result of an expression

```elixir
quote do: 1 + (2 + 3)
```

```elixir
quote do: 1 + unquote(2 + 3)
```

```elixir
number = 2
quote do: 1 + number
```

```elixir
number = 2
quote do: 1 + unquote(number)
```

```elixir
defmodule M do
  def f do
    2 + 3
  end
end

quote do: 1 + M.f()
```

```elixir
defmodule M do
  def f do
    2 + 3
  end
end

quote do: 1 + unquote(M.f())
```

```elixir
defmodule M do
  def f do
    quote do: 2 + 3
  end
end

quote do: 1 + M.f()
```

```elixir
defmodule M do
  def f do
    quote do: 2 + 3
  end
end

quote do: 1 + unquote(M.f())
```

## Eval

```elixir
Code.eval_string("1+2")
```

## Apply

```elixir
# apply(module, function_name, args)
defmodule M do
  def f(param) do
    "hello " <> param
  end
end

# User atoms for the module and the function name
apply(M, :f, ["world"])
```
