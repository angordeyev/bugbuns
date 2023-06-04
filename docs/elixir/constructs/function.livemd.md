# Function

## Examples

```elixir
# Function
# Named function can have different arities for the same name
# Anonymous functions can have one arity for the name

# High order functions

execute = fn x -> x.() end
say_hello = fn -> IO.puts("hello") end

execute.(say_hello)

defmodule Hello do
  def world do
    IO.puts("Hello world")
  end
end

execute.(&Hello.world/0)

# Invoke dinamically

(fn -> IO.puts("dynamically") end).()

# Patten matching
matching = fn
  :ok -> IO.puts("OK MATCHED")
  :eror -> IO.puts("ERROR MATCHED")
end

matching.(:ok)
```

## Name Function Aguments When Calling

```elixir
defmodule M do
  def f(param1, param2) do
    {param1, param2}
  end
end

M.f(_param1 = 1, _param2 = 2)
```

## Default Parameters

[Elixir Forum - What do function heads accomplish in the case of default arguments?](https://elixirforum.com/t/what-do-function-heads-accomplish-in-the-case-of-default-arguments/3004/4)

## Default Parameters Example 1

```elixir
defmodule M do
  def f(param \\ :default) do
    # IO.inspect(param1, label: "param1")
    IO.puts("param: #{param}")
  end
end

M.f(:value)
M.f()

:ok
```

## Default Parameters Example 2

```elixir
defmodule M do
  def f(param1, param2 \\ :default2) do
    IO.puts("param1: #{param1}, param2: #{param2}")
  end
end

M.f(:value1, :value2)
M.f(:value1)

:ok
```

## Default Parameters Example 3

```elixir
defmodule M do
  def f(param1 \\ :default1, param2 \\ :default2) do
    IO.puts("param1: #{param1}, param2: #{param2}")
  end
end

M.f(:value1, :value2)
M.f(:value)
M.f()

:ok
```

## Default Parameters Example 4

```elixir
defmodule M do
  def f(param1 \\ :default1, param2) do
    IO.puts("param1: #{param1}, param2: #{param2}")
  end
end

M.f(:value1, :value2)
M.f(:value)

:ok
```

## Default Parameters Example 5

```elixir
defmodule M do
  def f(param1, param2 \\ :default2, param3, param4 \\ :default4) do
    IO.puts("param1: #{param1}, param2: #{param2}, param3: #{param3}, param4: #{param4}")
  end
end

M.f(:value1, :value2, :value3, :value4)
# default value is used for the last parameter
M.f(:value1, :value2, :value3)
M.f(:value1, :value2)

:ok
```

## Function Head

```elixir
# See warning is generated
defmodule M do
  def f(1, param2 \\ :default) do
    param2
  end

  def f(2, param2) do
    param2
  end
end
```

This one should work.

```elixir
defmodule M do
  # This bodyless defenition is called function head
  # Elixir allows defaults to be declared only once in the head function
  def f(param1, param2 \\ :default)

  def f(1, param) do
    param
  end

  def f(2, param) do
    param
  end
end
```

This module will not compile.

```elixir
try do
  defmodule M do
    def f(1, param \\ :default) do
      param
    end

    def f(2, param \\ :default) do
      param
    end
  end
rescue
  error ->
    IO.puts(error.description)
    :ok
end
```

## Anonymous functions

```elixir
some_function = fn -> IO.puts("hi") end
some_function.()

# With multiple patterns
f = fn
  1 -> :ok
  2 -> :error
end
```
