## Behaviours

Define behaviour

```elixir
defmodule Greet do
  @callback greet(String.t) :: String.t
end
```

Terminology:

There is a behaviour module which defines an interace and callback module which defines implementation.
`@callback` defines callback functions which should be implemented in a callback module.

Implementation

```elixir
defmodule WorldGreeter do
  @behaviour Greet

  @impl true
  def greet(name) do
    "Hello #{name}"
  end
end
```

Error implementation

```elixir
defmodule WorldGreeter do
  @behaviour Greet_error

  @impl true
  def greet(name) do
    "Hello #{name}"
  end
end
```

```shell
mix compile --force
```
```output
warning: @behaviour Greet_error does not exist (in module WorldGreeter)
```

```shell
mix dialyzer
```
```output
Callback info about the Greet_error behaviour is not available.
```

```elixir
defmodule WorldGreeter do
  @behaviour Greet

  def greet_error(name) do
    "Hello #{name}"
  end
end
```

```shell
mix compile --force
```
```output
function greet/1 required by behaviour Greet is not implemented
```

```shell
mix dialyzer
```
```output
Undefined callback function greet/1 (behaviour Greet).
```

Implementing multiple behaviours

```elixir
defmodule Hello do
  @callback hello(String.t) :: String.t
end

defmodule Bye do
  @callback bye(String.t) :: String.t
end

defmodule PersonalMessages do
  @behaviour Hello
  @behaviour Bye

  @impl Hello
  def hello(name) do
    "hello #{name}"
  end

  @impl true # implements Hello or Bye behaviour
  def bye(name) do
    "bye #{name}"
  end
end

# no compile and dialyzer errors
```

With errors

```elixir
defmodule PersonalMessages do
  @behaviour Hello
  @behaviour Bye

  @impl Bye
  def hello(name) do
    "hello #{name}"
  end

  def bye(name) do
    "bye #{name}"
  end

  @impl true
  def greet(name) do
    "greeting #{name}"
  end
end
```

```shell
mix compile --force
```
```output
warning: got "@impl Bye" for function hello/1 but this behaviour does not specify such callback. The known callbacks are:

warning: got "@impl true" for function greet/1 but no behaviour specifies such callback. The known callbacks are:
 * Bye.bye/1 (function)
 * Hello.hello/1 (function)

warning: module attribute @impl was not set for function bye/1 callback (specified in Bye). This either means you forgot to add the "@impl true" annotation before the definition or that you are accidentally overriding this callback
```

```shell
mix dialyzer
```
```output
done (passed successfully) # dialyzer does not check behaviours
```

Implementing an inheritance:

```elixir
defmodule Greet do
  @callback greet(String.t) :: String.t

  def greet(name) do # you can define implementation in the beheviour module as well
    "hello #{name}"
  end
end

defmodule WorldGreeter do
  @behaviour Greet

  @impl true
  defdelegate greet(name), to: Greet
end
```

Behaviour and multiple functions implementation (pattern matching):

```elixir
defmodule Greet do
  @callback greet(String.t) :: String.t
end

defmodule WorldGreeter do
  @behaviour Greet

  @impl true
  def greet("") do
    "hello"
  end

  @impl true
  def greet(name) do
    "hello #{name}"
  end
end
```

Read more here [@impl docs](https://hexdocs.pm/elixir/1.13/Module.html#module-impl)
