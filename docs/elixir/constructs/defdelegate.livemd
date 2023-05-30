# defdelegate

## Example

```elixir
defmodule Hello do
  # Delegates greet() function to `World.greet()` function
  defdelegate greet, to: World

  # Delegates world() function to `World.greet()` function, different function name
  defdelegate world, to: World, as: :greet
end

defmodule World do
  def greet() do
    "hello world"
  end
end

{
  Hello.greet(),
  Hello.world()
}
```
