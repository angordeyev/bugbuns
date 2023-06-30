# Elixir

Elixir as Constructor

## Getting Help

* [hexdocs.pm](https://hexdocs.pm/)
* `iex> h`

## use, import, require, alias

### Alias

Defines new name for Atom, the name should start with Upper Letter

    iex> alias :a, as: A
    iex> A
    :a

    alias Math.List # same as alias Math.List, as: List
    List # Math.List

    iex> alias :a, as: :b # Error

### Import

Allows to use public module functions without module name

    import List
    first([1, 2, 3]) # 1

Import to use functions without module name

    iex> import List # imports all functions
         import List, only: [first: 2] # import only one function "List.first/2"

    iex> first([1,2,3], "default")
    1

    iex> first([1,2,3]) # only List.first/2 is imported
    ** (CompileError) iex:4: undefined function first/1 (there is no such import)

Importing module automatically requires it

    iex> import Logger
    iex> info("hello")
    [info] hello
    :ok

Use to extend module

    defmodule Chucky.Server do
      use GenServer

      ...

    end

Require to use macro

    require Integer

    Integer.is_odd(1)

## Application

The application is defined in `./mix.exs` file

    defmodule Example.MixProject do
      use Mix.Project

      def project do
        [
          app: :example,
          version: "1.2.3",
          ...
        ]
      end

      def application do
          [mod: {Example.Application, []}, extra_applications: [:logger]]
      end
      ...
    end

Then it is converted to `_build/dev/lib/example/ebin/example.app`

    {application,example,
        [{compile_env,[{example,['Elixir.HelloPhoenixWeb.Gettext'],error}]},
         {applications,
             [kernel,stdlib,elixir,logger]},
         {description,"example"},
         {modules,
             ['Elixir.Example',
              'Elixir.Example.Application',
              ....
              'Elixir.Example.Repo']},
         {registered,[]},
         {vsn,"1.2.3"},
         {mod,{'Elixir.Example.Application',[]}}]}.


The application module `./lib/example/application.ex`

    defmodule Example.Application do

      use Application

      @impl true
      def start(_type, _args) do
        children = [
          ClusterExample.Repo,
          ClusterExampleWeb.Endpoint
        ]
        opts = [strategy: :one_for_one, name: ClusterExample.Supervisor]
        Supervisor.start_link(children, opts)
      end
    end

### extra_applications

Required to start applications which are part of Elixir ditribution.
Other applications are started automatically

## Data types

A piece of data of any data type is called a term[4^].

There are two major types of terms:
- immediate terms which require no heap space (small integers, atoms, pids)
- cons or boxed terms (tuple, big num, binaries etc) that do require heap space.

### Arithmetic

    30 # 30, decimal
    0x1E # 30, hex
    0b11110 # 30, binary
    0o36 # 30, octal

Separator

Can be used for thousands

    1_000 # 1000

But it works in other places as well

    1_00 # 100
    0x00_0A # 10
    0b0000_0001 # 1

### Atoms

    is_atom(:atom) # true
    is_atom(Atom) # true
    is_atom(false) # true
    is_atom(:"123") # true
    is_atom(1) # false
    is_atom("atom") # false

All uppercase atoms in Elixir automatically receive the Elixir. prefix.

    List == :"Elixir.List"
    :"Elixir.List".first([1,2,3]) # 1

Because List is just an alias

    alias :"Elixir.List", as: List

If charlist is used when defining an atom it is converted to binary

    :"123" == :'123' # true
    :'123' # :"123"

Maximum number of atoms:

    :math.pow(2,20) == 1048576 # true
    :erlang.system_info(:atom_limit) == 1048576 # default

Atoms limit can be increased

    iex --erl "+t 2097152" # 8192-2 147483647

Atom uses one word

### Binary

**Bitstrings**

8 bits are used by default for each element in BitString

    <<1, 0x02, "a">> # <<1, 2, 97>>
    <<255, 256, 257>> # <<255, 0, 1>>, 256 does not fit and starts again from 0

Number of bits can be set using `::n` expression

    <<1::1>> == <<1::size(1)>> # true, shortcut expression
    <<1::1, 1::1>> == <<3::size(2)>> # true
    <<1::4, 1::4>> # << 17 >>, full 8 bits
    <<255::16, 256::16, 257::16>> # <<0, 255, 1, 0, 1, 1>>

**Binary** is a bitstring where the number of bits is divisible by 8

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

Match to binary

    iex> <<first::binary-size(1), second::binary-size(2), rest::binary>> = "123___"
    "123___"

    iex> {first, second, rest}
    {"1", "23", "___"}

    # Pattern match does not work without rest binary
    iex> <<first::binary-size(1), second::binary-size(2)>> = "123___"
    ** (MatchError) no match of right hand side value: "123___"

**Double quotes strings**

    "12" == << 49, 50 >> # true

**Concatenation**

    "a" <> "b" # ab
    <<1>> <> <<2>> # <<1, 2>>

### Tuple

    {1, :a, Temp}

Is like array and uninterrupted, or continuously in memory.

### List

    [1, :a, Temp]

### Keyword list

Elixir keyword list is shortcut for a list tuples

    iex> keyword_list = [{:a, 1}, {:b, 2}] # same as below
    [a: 1, b: 2]

    iex> keyword_list = [{A, 1}, b: 2] # same as below, no short syntax
    [{A, 1}, {:b, 2}] #

Elements can be accessed like this:

    keyword_list = [{A, 1}, b: 2]
    [{A, 1}, {:b, 2}]


    iex> keyword_list[A]
    1

    iex> keyword_list[:b]
    2

    iex> keyword_list[:c]
    nil

    iex> Keyword.get(keyword_list, A)
    1

    iex> Keyword.get(keyword_list, :b)
    2

    iex> Keyword.get(keyword_list, :c)
    nil

    iex> Keyword.fetch(keyword_list, A)
    {:ok, 1}

    iex> Keyword.fetch(keyword_list, :b)
    {:ok, 2}

    iex> Keyword.fetch(keyword_list, :c)
    :error

    iex> Keyword.fetch!(keyword_list, A)
    1

    iex> Keyword.fetch!(keyword_list, :b)
    2

    iex> Keyword.fetch!(keyword_list, :c)
    (KeyError) key :c not found in: [{A, 1}, {:b, 2}]



but

    keyword_list.a # Error: left side should be atom or map

**Keyworld list** can we used in in list and map but it shoud go last

Lists

    [{:a, 1}, b: 1, c: :d] # [a: 1, b: 1, c: :d]

    [1, {:a, 1}, b: 1] # [1, {:a, 1}, {:b, 1}]

    [a: 1, {:b, 1}] # Error: Keyword lists must always come last in lists and maps

Maps

    %{:a => 1, b: 2} # %{a: 1, b: 2}

    %{a: 1, :b => 2} # Error: Keyword lists must always come last in lists and maps

Call syntax

When keyword list is passed as the last argument when calling a function, square bracket can be ommited

    IO.inspect a: 1, b: 2 # [a: 1, b: 2]
    IO.inspect(a: 1, b: 2) # [a: 1, b: 2]
    String.split " a b c ", " ", trim: true # ["a", "b", "c"]

    IO.inspect(a: 1, b: 2, label: "test") # [a: 1, b: 2, label: "test"],
                                          # label: "test" is treated as the part of signle parameter
    IO.inspect([a: 1, b: 2], label: "test") # [a: 1, b: 2]

Do block is a keyword list

    iex> [{:do, "Done"}, {:else, "Other"}]
    [do: "Done", else: "Other"]

### Map

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

### Structs

Structs are maps

Stucts and maps starts with `%` sign

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

Error check

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

#### Ranges

Definition

    iex> 1..3
    1..3

    iex> 1..10//2
    1..10//2

    iex> Range.new(1,10,2) # using function
    1..10//2

    iex> a = 1; b = 5; a..b
    1..5

Ranges are stored as structs

Pattern matching

    iex> first..last//step = 1..10/2
    1..10//2

    iex> first..last//step = 1..10
    1..10//2
    iex>{first, last, step}
    {1,10,1}

Range implements Enumerable protocol
Reduce

    iex> Enum.reduce(1..3, 0, fn i, acc -> acc + i end)
    6

## Language constructions

## Sigils[^3]

Sigils are normaly used with () delimiters althought the following delimiters are available:
`//, ||, "", '', (), [], {}, <>`

    ~s("hello") # "\"hello\""
    ~D[2020-12-31] # ~D[2020-12-31], date
    ~w(hello world) # ["hello", "world"], world list
    ~w"hello world" # ["hello", "world"], world list
    ~w"hello world"a # [:hello, :world], a - atom parameter
    ~w(hello #{1+1}) # ["hello", "2"], with inerpolation
    ~W(hello #{1+1}) # ["hello", "\#{1+1}"], without interpolation

Same as

    sigil_w(<<"hello world">>, 's') # ["hello", "world"] # s - strings
    sigil_w(<<"hello world">>, 'a') # [:hello, :world]   # a - atoms

Getting help

    h sigil_w

Defining own sigils is simple

    defmodule SemicolonList do
      def sigil_x(string, [])do
        String.split(string, ";")
      end
    end

    import SemicolonList

    ~x(1;2) # ["1", "2"]

## Documentation

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

Then you can read documentation

    h HelloDocs
    h HelloDocs.hello

## JSON encoding/decoding

Encoding

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

Decoding

    iex> Jason.decode!(~s({"a":1,"b":"bb"}))
    %{"a" => 1, "b" => "bb"}

## Environments

    MIX_ENV=test
    MIX_ENV=dev
    MIX_ENV=prod

E.g. to rest test migration

    MIX_ENV=test mix ecto.reset

## Reference

[^2]: IEx - interactive Elixir; pry - вмешиваться
[^3]: sigil - символ (кельтский символ, символ льва)
[^4]: In mathematical logic, a term denotes a mathematical object while a formula denotes a mathematical fact. (wikipedia)


