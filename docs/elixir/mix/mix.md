# Mix

Mix is a build tool that provides tasks for creating, compiling, and testing
Elixir projects. Mix unit is called "task".

## Getting Help

Print istalled tasks and their description:

```shell
mix help
```

Print tasks started with prefix:

```shell
mix phx
mix phx.gen
```

Get help for the task:

```shell
mix help phx.new
```

Open [Mix Docs](https://hexdocs.pm/mix/Mix.html) or go to [hexdocs.pm](https://hexdocs.pm) and search for `mix` or  for the web docs.

## Tasks

### Working with Depencencies

List deps tasks:

```shell
mix help | grep "deps\."
```

Get help for a task:

```shell
mix help deps.clean
```

### Remove Unused Dependencies

```shell
mix deps.clean --unlock --unused
```

### Custom mix Task

[Elixir School - Custom Mix Tasks](https://elixirschool.com/en/lessons/intermediate/mix_tasks)

Generate a new project

```shell
mix new custom_mix_task
```

Create a Mix task at `lib/mix/tasks/hello.ex`

```elixir
defmodule Mix.Tasks.Hello do
  use Mix.Task

  def run(param) do
    IO.puts("Hello #{param}")
  end
end
```

Run Mix task

```shell
mix hello World
```
```output
Hello World
```

To run application add to the mix task

```elixir
def run(_) do
  ...
  Mix.Task.run("app.start")
  ...
end
```

### Debugging Mix Tasks

To debug a custom Mix task use can use `require IEx; IEx.pry()`:

```elixir
defmodule Mix.Tasks.Hello do
  use Mix.Task

  def run(param) do
    require IEx; IEx.pry()
    IO.puts("Hello #{param}")
  end
end
```

Then run a task (for Erlang 26 and later):

```shell
mix hello
```

Then run a task (for Erlang 25 and older):

```shell
iex -S mix hello
```

## Creating own Mix Archives

Create a new project

```shell
mix new hello_build
```

Create a Mix task at `mix/tasks/hello.ex`

```elixir
defmodule Mix.Tasks.Hello do
  use Mix.Task

  def run(param) do
    IO.puts("Hello #{param}")
  end
end
```

Build archive

```shell
mix archive.build
```

`hello_build-0.1.0.ez` file will be created in the project directory (.ez is zip archive)

Install an archive:

```shell
mix archive.install hello_build-0.1.0.ez
```

Check if archive is installed

```shell
mix archive
```
```output
...
* hello_build-0.1.0
...
```

Test an archive:

```shell
mix hello World
```
```output
Hello World
```

Uninstall an archive:

```shell
mix archive.uninstall hello_build-0.1.0
```

## mix.exs

### deps

Read more in [the official docs](https://hexdocs.pm/mix/1.13/Mix.Tasks.Deps.html).

Make the dependency available only in the given environment:

```elixir
{:phoenix_live_reload, "~> 1.2", only: :dev},
```

Do not run the application:

```elixir
{:credo, "~> 1.6", only: [:dev, :test], runtime: false}
```

Run the application only in the provided environment:

```elixir
{:esbuild, "~> 0.3", runtime: Mix.env() == :dev}
```

## Dependency resoultion

Errors

```output
Resolving Hex dependencies...

Failed to use "mime" (versions 2.0.0 to 2.0.2) because
  bamboo (version 2.2.0) requires ~> 1.4
  phoenix_live_dashboard (version 0.6.5) requires ~> 1.6 or ~> 2.0


Failed to use "ranch" (version 1.7.1) because
  bamboo_smtp (version 4.2.0) requires 2.0.0
  bypass (version 2.1.0) requires ~> 1.3
  mix.exs specifies ~> 1.7.1


Failed to use "ranch" (version 1.7.1) because
  bypass (version 2.1.0) requires ~> 1.3
  cowboy (version 2.8.0) requires ~> 1.7.1
  gen_smtp (version 1.2.0) requires >= 1.8.0
  mix.exs specifies ~> 1.7.1
```

Solution (add `override: true` for the package which is failed to use)

```elixir
{:ranch, "~> 1.7.1", , override: true}
```

## Resources

[Create a Mix Task for an Elixir Project](http://joeyates.info/2015/07/25/create-a-mix-task-for-an-elixir-project/)
