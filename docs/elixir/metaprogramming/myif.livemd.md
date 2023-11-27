# My If

## Code

```elixir
defmodule MyIf do
  defmacro my_if(expr, my: if_block) do
    quote do
      if unquote(expr) do
        unquote(if_block)
      end
    end
  end
end
```

```elixir
import MyIf
my_if(true, my: IO.puts("hello"))
```

```elixir
defmodule Control do
  defmacro my_if_else(expr, do: if_block, else: else_block) do
    quote do
      if unquote(expr) do
        unquote(if_block)
      else
        unquote(else_block)
      end
    end
  end
end
```

```elixir
import Control
my_if_else(true, do: IO.puts("hello if"), else: IO.puts("hello else"))
```

```elixir
import Control

my_if_else true do
  IO.puts("hello if")
else
  IO.puts("hello else")
end

my_if_else false do
  IO.puts("hello if")
else
  IO.puts("hello else")
end
```

```elixir
quote do
  some_if true do
    IO.puts("hi")
    some_else
    IO.puts("bye")
  end
end

quote do
  if true do
    IO.puts("hi")
  else
    IO.puts("bye")
  end
end
```

```elixir
defmodule MyMacro do
  defmacro assert_refute(do: if_block, after: else_block) do
    quote do
      unquote(if_block)
      :timer.sleep(2000)
      unquote(else_block)
    end
  end
end
```

```elixir
import MyMacro

assert_refute do
  IO.puts("hi")
after
  IO.puts("bye")
end
```
