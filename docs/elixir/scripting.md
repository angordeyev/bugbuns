# Scripting

## Simple script

Create the file:

```elixir title="simple_script.exs"
IO.puts("hi")
```

Run it

```shell
elixir simple_script.exs
```
```output
hi
```

## With dependencies:

Create the file:

```elixir title="with_dependencies.exs"
Mix.install([
  {:httpoison, "~> 1.8"}
])

HTTPoison.start()

"example.com"
|> HTTPoison.get!()
|> IO.inspect()
```

Run it:

```shell
elixir simple_script.exs
```
```output
%HTTPoison.Response{....}
```

## Resources

[Building CLI scripts with Elixir](https://nick.groenen.me/notes/building-cli-scripts-with-elixir/)
