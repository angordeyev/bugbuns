## Scripting

### Simple script

Create file `simple_script.exs`

    IO.puts("hi")

Run it

    ➜ elixir simple_script.exs
    hi

### With dependencies

Create file `with_dependencies.exs`

    Mix.install([
      {:httpoison, "~> 1.8"}
    ])

    HTTPoison.start()

    "example.com"
    |> HTTPoison.get!()
    |> IO.inspect()


Run it

    ➜ elixir simple_script.exs
    %HTTPoison.Response{....}

### Resources

[Building CLI scripts with Elixir](https://nick.groenen.me/notes/building-cli-scripts-with-elixir/)
