# Protocol

## Implement protocol

```elixir
defmodule N do
  defstruct a: "a", b: "b"
end

defimpl String.Chars, for: N do
  def to_string(_) do
    "1"
  end
end

defmodule M do
  defstruct a: "a", b: "b"

  defimpl String.Chars, for: M do
    def to_string(_) do
      "2"
    end
  end
end

defmodule Example do
  @moduledoc """
  Stucts can be used in other context that is whey Example module is defined
  """

  def main() do
    IO.inspect(%N{})
    IO.inspect(%M{})
    IO.puts(%N{})
    IO.puts(%M{})
    :ok
  end
end

Example.main()
```

## Own Protocol

```elixir
defprotocol P do
  def main(t)
end

defimpl P, for: BitString do
  def main(_) do
    "1"
  end
end

defimpl P, for: Integer do
  def main(_) do
    "2"
  end
end

defmodule Example do
  def main() do
    IO.inspect(P.main("hello"))
    IO.inspect(P.main(100))
    :ok
  end
end

Example.main()
```

## Usign Protocol Directly

```elixir
# String.Chars protocol is implemented for Integer and List

[
  String.Chars.to_string(1),
  String.Chars.to_string([1, 2, 3])
]
```

```elixir
# String.Chars protocol is not implemented for Tuple and Map

try do
  String.Chars.to_string({1, 2})
rescue
  error -> IO.inspect(error)
end

try do
  String.Chars.to_string(%{a: 1, b: 2})
rescue
  error -> IO.inspect(error)
end
```
