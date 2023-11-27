# Typespecs

## Typespecs attributes

- `@type`
- `@opaque`
- `@typep`
- `@spec`
- `@callback`
- `@macrocallback`

## Using IEx

To list the built-in types:

    iex> t :erlang # list all types

    iex> t :erlang. # autocomplete will work and allow to select type

    iex> t :erlang.boolean
    @type boolean() :: true | false

    iex> t :erlang.bool
    @type bool() :: boolean(

    iex> t :erlang.pos_integer
    @type pos_integer() :: pos_integer()

List types defined in a module:

    iex> t String
    @type codepoint() :: t()

    @type grapheme() :: t()

    @type pattern() :: t() | [t()] | :binary.cp()

    @type t() :: binary()

Show a type information:

    iex> t String.t
    @type t() :: binary()

    A UTF-8 encoded binary.

    The types String.t() and binary() are equivalent to analysis tools. Although,
    for those reading the documentation, String.t() implies it is a UTF-8 encoded
    binary.

## Check Typescpecs

Required dependences:

```elixir
{:dialyxir, "~> 1.4"}
```

Check with dializer:

```shell
mix dialyzer
```

The example:

```elixir
defmodule HelloTypespecs do
  def work do
    try do
      sum("a", "b")
    rescue _e ->
      :ok
    end
  end


  @spec sum(integer, integer) :: integer
  def sum(_a, _b) do
    1
  end
end
```

```shell
mix dialyzer
```
```output
lib/hello_typespecs.ex:4:call
The function call will not succeed.

HelloTypespecs.sum(<<97>>, <<98>>)

breaks the contract
(integer(), integer()) :: integer()
```

## Defining Typespecs

Using

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

Defining own types

    defmodule A do
      @type word() :: String.t()
    end

    iex> t A
    @type t() :: binary()

Type docs

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

## Examples

### Simple

```elixir
defmodule Atom do
  ...
  @spec to_string(atom) :: String.t()
  def to_string(atom) do
      :erlang.atom_to_binary(atom)
  end
  ...
end
```

### Single Spec for a Function with Multiple Matches

```elixir
...
defmodule Enum do
  @spec join(t, binary()) :: binary()
  def join(enumerable, joiner \\ "")

  def join(enumerable, "") do
    ...
  end

  def join(enumerable, joiner) when is_binary(joiner) do
    ...
  end
end
```

### Overloaded function

### Cases

#### `String.t()` or `binary()`

Strint.t() is UTF8 encoded binary

> The types `String.t()` and `binary()` are equivalent to analysis tools.
> Although, for those reading the documentation, `String.t()` implies
> it is a UTF-8 encoded binary.
>
> -- <cite>[String.t(). Elixir Docs.](https://hexdocs.pm/elixir/String.html#t:t/0)</cite>
## Resouces

[Typespecs. Elixir Docs.](https://hexdocs.pm/elixir/1.15.7/typespecs.html)
