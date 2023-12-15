# Mix

Mix is a build tool that provides tasks for creating, compiling, and testing
Elixir projects. Mix unit is called "task".

## Getting Help

Print tasks and their description

```shell
mix help
```

Go to [hexdocs.pm](https://hexdocs.pm) and search for `mix` or open [hexdocs.pm/mix/Mix.html](https://hexdocs.pm/mix/Mix.html) for the web docs.

Get help for the task

```shell
mix help phx.new
```

## Working with mix Archives

### Commands

List archives:

```shell
mix archive
```

Install a hex archive:

```shell
mix archive.install hex <package>
mix archive.install hex <package> <version>
```

Install a local archive

```shell
mix archive.install archive.ez
mix archive.install path/to/archive.ez
```

Install GitHub archive

```shell
mix archive.install git https://path/to/git/repo
mix archive.install git https://path/to/git/repo branch git_branch
```

Uninstall an archive

```shell
mix archive.uninstall <package>
```

### Examples

```shell
mix archive.install hex phx_new
```

```shell
mix archive
```
```output
* hex-1.0.1
* phx_new-1.6.11
```

```shell
mix archive.uninstall phx_new
```

```shell
mix archive
```
```output
* hex-1.0.1
```

```shell
mix archive.install hex phx_new
```

## Tasks

### Remove Unused Dependencies

```shell
mix deps.clean --unlock --unused
```

## Custom mix Task

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
