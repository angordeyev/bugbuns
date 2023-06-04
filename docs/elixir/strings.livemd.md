# Strings

## Bitstring

```elixir
IO.inspect(<<1, 0x02, "a">>)
# 256 does not fit and starts again from 0
IO.inspect(<<255, 256, 257>>)
:ok
```

```elixir
# Number of bits can be set using `::n` expression
# true, shortcut expression
IO.inspect(<<1::1>> == <<1::size(1)>>)
# true
IO.inspect(<<1::1, 1::1>> == <<3::size(2)>>)
# << 17 >>, full 8 bits
IO.inspect(<<1::4, 1::4>>)
# <<0, 255, 1, 0, 1, 1>>
IO.inspect(<<255::16, 256::16, 257::16>>)
:ok
```

## Binary

**Binary** is a bitstring where the number of bits is divisible by 8

```elixir
# true
IO.inspect(<<100>> == <<100::8>>)
# true
IO.inspect(is_bitstring("a"))
# true
IO.inspect(is_bitstring(<<100>>))
# true
IO.inspect(is_bitstring(<<100::4>>))
# true
IO.inspect(is_bitstring(<<100::8>>))
# true
IO.inspect(is_bitstring(<<100::16>>))
:ok
```

```elixir
# true
IO.inspect(is_binary("a"))
# true
IO.inspect(is_binary("п"))
# true
IO.inspect(is_binary(<<100>>))
# true
IO.inspect(is_binary(<<100::16>>))
# true
IO.inspect(is_binary(<<1::4, 1::4>>))
# false
IO.inspect(is_binary(<<100::4>>))
:ok
```

## Match to binary

```elixir
<<first::binary-size(1), second::binary-size(2), rest::binary>> = "123___"
IO.inspect([first, second, rest])
:ok
```

Pattern match does not work without rest binary

```elixir
try do
  <<_first::binary-size(1), _second::binary-size(2)>> = "123___"
rescue
  _e -> :error
end
```

## Heredoc

Ending with new line

```elixir
"""
123
 456
"""
```

Without new line

```elixir
String.trim_trailing("""
123
 456
""")
```
