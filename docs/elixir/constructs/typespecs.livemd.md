# Typespecs

## General Information

Typespecs attributes:

* `@type`
* `@opaque`
* `@typep`
* `@spec`
* `@callback`
* `@macrocallback`

To list built-in types

```
iex> t :erlang # list all types

iex> t :erlang. # autocomplete will work and allow to select type

iex> t :erlang.boolean
@type boolean() :: true | false

iex> t :erlang.bool
@type bool() :: boolean(

iex> t :erlang.pos_integer
@type pos_integer() :: pos_integer()
```

List types defined in module

```
iex> t String
@type codepoint() :: t()

@type grapheme() :: t()

@type pattern() :: t() | [t()] | :binary.cp()

@type t() :: binary()
```

Show one type information

```
iex> t String.t
@type t() :: binary()

A UTF-8 encoded binary.

The types String.t() and binary() are equivalent to analysis tools. Although,
for those reading the documentation, String.t() implies it is a UTF-8 encoded
binary.
```

Using

```
defmodule Math do
  @spec sum(integer, integer) :: integer
  def sum(a, b) do
    a + b
  end

  def mult(a, b) do
    a * b
  end
end

iex> h Math.sum
def sum(a, b)
@spec sum(integer(), integer()) :: integer()
```

Specs will be checked with Dializer `mix dialyzer`

```
defmodule Hello do
  def work do
    Math.sum("a", "b")
  end
end

defmodule Math do
  @spec sum(integer, integer) :: integer
  def sum(a, b) do
    "some string"
  end
end

$ mix dialyzer
_____________________________________________________________________________________
Error: The function call will not succeed.
Math.sum(<<97>>, <<98>>)
will never return since the 1st and 2nd arguments differ
from the success typing arguments:
_____________________________________________________________________________________
Error: invalid_contract
The @spec for the function does not match the success typing of the function.
Function: Math.sum/2
Success typing:
@spec sum(integer(), integer()) :: binary()
_____________________________________________________________________________________
```

Defining own types

```
defmodule A do
  @type word() :: String.t()
end

iex> t A
@type t() :: binary()
```

Type docs

```
defmodule A do
  @typedoc """
  Single word
  """
  @type word() :: String.t()
end

iex> t A # show types without docs
@type word() :: String.t()

iex> t A.word # show type with docs
@type word() :: String.t()
Single word
```

## Examples

```elixir
defmodule Math do
  @spec sum(integer, integer) :: integer
  def sum(a, b) do
    a + b
  end
end

Math.sum("a", "b")
```
