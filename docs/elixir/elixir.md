# Elixir

Elixir as Constructor

## use, import, require, alias

### Alias

Defines new name for Atom, the name should start with Upper Letter:

```elixir
iex> alias :a, as: A
iex> A
```
```output
:a
```

```elixir
alias Math.List # same as alias Math.List, as: List
List # Math.List

iex> alias :a, as: :b # Error
```

### Import

Allows to use public module functions without module name:

```elixir
import List
first([1, 2, 3]) # 1
```

Import to use functions without module name:

```elixir
    iex> import List # imports all functions
         import List, only: [first: 2] # import only one function "List.first/2"
```

```elixir
    iex> first([1,2,3], "default")
```
```output
1
```

```elixir
iex> first([1,2,3]) # only List.first/2 is imported
```
```output
    ** (CompileError) iex:4: undefined function first/1 (there is no such import)
```

Importing a module automatically requires it:

```elixir
iex> import Logger
iex> info("hello")
```
```output
[info] hello
:ok
```

Use to extend module:

```elixir
defmodule Chucky.Server do
  use GenServer

  ...

end
```
Require to use macro

```elixir
require Integer

Integer.is_odd(1)
```

## Data types

A piece of data of any data type is called a term[4^].

There are two major types of terms:
- immediate terms which require no heap space (small integers, atoms, pids)
- cons or boxed terms (tuple, big num, binaries etc) that do require heap space.

### Arithmetic

```elixir
30 # 30, decimal
0x1E # 30, hex
0b11110 # 30, binary
0o36 # 30, octal
```

Separator

Can be used for thousands:

```elixir
1_000 # 1000
```

But it works in other places as well:

```elixir
1_00 # 100
0x00_0A # 10
0b0000_0001 # 1
```

### Atoms

```elixir
is_atom(:atom) # true
is_atom(Atom) # true
is_atom(false) # true
is_atom(:"123") # true
is_atom(1) # false
is_atom("atom") # false
```

All uppercase atoms in Elixir automatically receive the `Elixir.` prefix:

```elixir
List == :"Elixir.List"
:"Elixir.List".first([1,2,3]) # 1
```

Because List is just an alias:

```elixir
alias :"Elixir.List", as: List
```

If charlist is used when defining an atom it is converted to binary:

```elixir
:"123" == :'123' # true
:'123' # :"123"
```

Maximum number of atoms:

```elixir
:math.pow(2,20) == 1048576 # true
:erlang.system_info(:atom_limit) == 1048576 # default
```

Atoms limit can be increased:

```elixir
iex --erl "+t 2097152" # 8192-2 147483647
```

Atom uses one word.

### Binary

**Bitstrings**

8 bits are used by default for each element in BitString:

```elixir
<<1, 0x02, "a">> # <<1, 2, 97>>
<<255, 256, 257>> # <<255, 0, 1>>, 256 does not fit and starts again from 0
```

Number of bits can be set using `::n` expression:

```elixir
<<1::1>> == <<1::size(1)>> # true, shortcut expression
<<1::1, 1::1>> == <<3::size(2)>> # true
<<1::4, 1::4>> # << 17 >>, full 8 bits
<<255::16, 256::16, 257::16>> # <<0, 255, 1, 0, 1, 1>>
```

**Binary** is a bitstring where the number of bits is divisible by 8:

```elixir
<<100>> == <<100::8>> # true
is_bitstring("a") # true
is_bitstring(<<100>>) # true
is_bitstring(<<100::4>>) # true
is_bitstring(<<100::8>>) # true
is_bitstring(<<100::16>>) # true

is_binary("a") # true
is_binary("п") # true
is_binary(<<100>>) # true
is_binary(<<100::16>>) # true
is_binary(<<1::4, 1::4>>) # true
is_binary(<<100::4>>) # false
```

Match to binary:

```elixir
iex> <<first::binary-size(1), second::binary-size(2), rest::binary>> = "123___"
```
```output
 "123___"
```

```elixir
iex> {first, second, rest}
```
```output
{"1", "23", "___"}
```

```elixir
# Pattern match does not work without rest binary
iex> <<first::binary-size(1), second::binary-size(2)>> = "123___"
```
```output
  ** (MatchError) no match of right hand side value: "123___"
```

**Double quotes strings**

```elixir
"12" == << 49, 50 >> # true
```

**Concatenation**

```elixir
"a" <> "b" # ab
<<1>> <> <<2>> # <<1, 2>>
```

### Tuple

```elixir
{1, :a, Temp}
```

Is like array and uninterrupted, or continuously in memory.

### List

```elixir
[1, :a, Temp]
```

### Keyword list

Elixir keyword list is shortcut for a list tuples

```elixir
iex> keyword_list = [{:a, 1}, {:b, 2}] # same as below
```
```output
[a: 1, b: 2]
```
```elixir
iex> keyword_list = [{A, 1}, b: 2] # same as below, no short syntax
```
```output
[{A, 1}, {:b, 2}] #
```

Elements can be accessed like this:

```elixir
keyword_list = [{A, 1}, b: 2]
```
```output
[{A, 1}, {:b, 2}]
```

```elixir
iex> keyword_list[A]
```
```output
1
```

```elixir
iex> keyword_list[:b]
```
```output
2
```

```elixir
iex> keyword_list[:c]
```
```output
nil
```


```elixir
iex> Keyword.get(keyword_list, A)
```
```output
1
```

```elixir
iex> Keyword.get(keyword_list, :b)
```
```output
2
```

```elixir
iex> Keyword.get(keyword_list, :c)
```
```output
nil
```

```elixir
iex> Keyword.fetch(keyword_list, A)
```
```output
{:ok, 1}
```

```elixir
iex> Keyword.fetch(keyword_list, :b)
```
```output
{:ok, 2}
```

```elixir
iex> Keyword.fetch(keyword_list, :c)
```
```output
:error
```

```elixir
iex> Keyword.fetch!(keyword_list, A)
```
```output
1
```

```elixir
iex> Keyword.fetch!(keyword_list, :b)
```
```output
2
```

```elixir
iex> Keyword.fetch!(keyword_list, :c)
```
```output
  (KeyError) key :c not found in: [{A, 1}, {:b, 2}]
```

but:

```elixir
keyword_list.a # Error: left side should be atom or map
```

**Keyworld list** can we used in in list and map but it shoud go last

Lists

```elixir

    [{:a, 1}, b: 1, c: :d] # [a: 1, b: 1, c: :d]

    [1, {:a, 1}, b: 1] # [1, {:a, 1}, {:b, 1}]

    [a: 1, {:b, 1}] # Error: Keyword lists must always come last in lists and maps

```

Maps

```elixir
    %{:a => 1, b: 2} # %{a: 1, b: 2}

    %{a: 1, :b => 2} # Error: Keyword lists must always come last in lists and maps
```

Call syntax

When keyword list is passed as the last argument when calling a function, square bracket can be ommited

```elixir
    IO.inspect a: 1, b: 2 # [a: 1, b: 2]
    IO.inspect(a: 1, b: 2) # [a: 1, b: 2]
    String.split " a b c ", " ", trim: true # ["a", "b", "c"]

    IO.inspect(a: 1, b: 2, label: "test") # [a: 1, b: 2, label: "test"],
                                          # label: "test" is treated as the part of signle parameter
    IO.inspect([a: 1, b: 2], label: "test") # [a: 1, b: 2]
```

Do block is a keyword list

```elixir
iex> [{:do, "Done"}, {:else, "Other"}]
```
```output
[do: "Done", else: "Other"]
```

### Map

```elixir
iex> m = %{1 => "value_1", :a => "value_a", Temp => TempValue}
%{1 => "value_1", Temp => TempValue, :a => "value_a"}

iex> m[1]
1

iex> m.a
"value_a"


iex> m[:a]
"value_a"

iex> Map.get(m, :a)
"value_a"

iex> Map.fetch(m, :a)
{:ok, "value_a"}

iex> Map.fetch!(m, :a)
"value_a"

iex> Map.get(m, :c)
nil

iex> Map.fetch(m, :c)
:error

iex> Map.fetch!(m, :c)
key :c not found in: %{1 => "value_1", Temp => TempValue, :a => "value_a"}

iex> m[Temp]
TempValue
```

### Structs

Structs are maps

Stucts and maps starts with `%` sign:

```elixir
defmodule User do
  defstruct [:name, :age]
end

defmodule User do
  defstruct name: nil, age: 18
end

defmodule User do
  defstruct [:name, age: 18] # keyword list shoud go las in the list, otherwise see below
end

defmodule User do
  defstruct [{:name, nil}, :age]
end

%User{} # %User{age: nil, name: nil}
%User{name: "Andrew", age: 20} # %User{age: nil, name: "Andrew"}
```

Error check:

```elixir
defmodule User do
  defstruct [:name, :age]
end

defmodule Hello do
  @spec work(User) :: String.t
  def work(user) do
    user.name
  end

  def test do
    Hello.work(%{name: "Andrey", age: 20})
  end
end
```

#### Ranges

Definition:

```elixir
iex> 1..3
1..3

iex> 1..10//2
1..10//2

iex> Range.new(1,10,2) # using function
1..10//2

iex> a = 1; b = 5; a..b
1..5
```

Ranges are stored as structs:

Pattern matching:

```elixir
iex> first..last//step = 1..10/2
1..10//2

iex> first..last//step = 1..10
1..10//2
iex>{first, last, step}
{1,10,1}
```

Range implements Enumerable protocol
Reduce

```elixir
iex> Enum.reduce(1..3, 0, fn i, acc -> acc + i end)
6
```

## Language constructions

## Sigils[^3]

Sigils are normaly used with () delimiters althought the following delimiters are available: `//, ||, "", '', (), [], {}, <>`

```elixir
~s("hello") # "\"hello\""
~D[2020-12-31] # ~D[2020-12-31], date
~w(hello world) # ["hello", "world"], world list
~w"hello world" # ["hello", "world"], world list
~w"hello world"a # [:hello, :world], a - atom parameter
~w(hello #{1+1}) # ["hello", "2"], with inerpolation
~W(hello #{1+1}) # ["hello", "\#{1+1}"], without interpolation
```

Same as:

```elixir
sigil_w(<<"hello world">>, 's') # ["hello", "world"] # s - strings
sigil_w(<<"hello world">>, 'a') # [:hello, :world]   # a - atoms
```

Getting help

```elixir
iex> h sigil_w
```

Defining own sigils is simple

```elixir
defmodule SemicolonList do
  def sigil_x(string, [])do
    String.split(string, ";")
  end
end

import SemicolonList

~x(1;2) # ["1", "2"]
```

## Documentation

```elixir
defmodule HelloDocs do
  @moduledoc """
  Documentation for `HelloDocs`.
  """

  @doc """
  Hello world.

  ## Examples

      iex> HelloDocs.hello()
      :world

  """
  def hello do
    :world
  end
end
```

Then you can read documentation

```elixir
iex> h HelloDocs
iex> h HelloDocs.hello
```

## JSON encoding/decoding

Encoding:

```elixir
iex> Jason.encode!(:a) == Jason.encode!("a")
true

iex> Jason.encode!(:a) == ~s("a")
true

iex> Jason.encode!(:a) == "\"a\""
true

iex> Jason.encode!(%{a: :aa, "b" => "bb"},)
"{\"a\":1}"

iex> Jason.encode!(%{a: 1}) == Jason.encode!(%{"a" => 1})
true
```

Decoding:

```elixir
iex> Jason.decode!(~s({"a":1,"b":"bb"}))
%{"a" => 1, "b" => "bb"}
```

## Environments

```shell
MIX_ENV=test
MIX_ENV=dev
MIX_ENV=prod
```

For example to reset test migration:

```shell
MIX_ENV=test mix ecto.reset
```

## Reference

[^2]: IEx - interactive Elixir; pry - вмешиваться
[^3]: sigil - символ (кельтский символ, символ льва)
[^4]: In mathematical logic, a term denotes a mathematical object while a formula denotes a mathematical fact. (wikipedia)
