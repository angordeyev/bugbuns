# mix

Mix is a build tool that provides tasks for creating, compiling, and testing
Elixir projects. Mix unit is called "task".

## Getting Help

Print tasks and their description

    mix help

Go to [hexdocs.pm](https://hexdocs.pm) and search for `mix` or open [hexdocs.pm/mix/Mix.html](https://hexdocs.pm/mix/Mix.html) for the web docs.

Get help for the task

    mix help phx.new

## Working with mix Archives

### Commands

List archives

    mix archive

Install hex archive

    mix archive.install hex <package>
    mix archive.install hex <package> <version>

Install local archive

    mix archive.install archive.ez
    mix archive.install path/to/archive.ez

Install GitHub archive

    mix archive.install git https://path/to/git/repo
    mix archive.install git https://path/to/git/repo branch git_branch

Uninstall archive

    mix archive.uninstall <package>

### Examples

    mix archive.install hex phx_new

    mix archive
    * hex-1.0.1
    * phx_new-1.6.11

    mix archive.uninstall phx_new

    mix archive
    * hex-1.0.1

    mix archive.install hex phx_new

    mix archive
    * hex-1.0.1
    * phx_new-1.6.11

## Tasks

### Remove Unused Dependencies

    mix deps.clean --unlock --unused

## Custom mix Task

[Elixir School - Custom Mix Tasks](https://elixirschool.com/en/lessons/intermediate/mix_tasks)

Generate a new project

    mix new custom_mix_task

Create a Mix task at `lib/mix/tasks/hello.ex`

    defmodule Mix.Tasks.Hello do
      use Mix.Task

      def run(param) do
        IO.puts("Hello #{param}")
      end
    end

Run Mix task

    mix hello World
    Hello World

To run application add to the mix task

    def run(_) do
      ...
      Mix.Task.run("app.start")
      ...
    end

### Debugging Mix Tasks

To debug a custom Mix task use can use `require IEx; IEx.pry()`:

    defmodule Mix.Tasks.Hello do
      use Mix.Task

      def run(param) do
        require IEx; IEx.pry()
        IO.puts("Hello #{param}")
      end
    end

Then run a task (for Erlang 26 and later):

    mix hello

Then run a task (for Erlang 25 and older):

    iex -S mix hello

## Creating own Mix Archives

Create a new project

    mix new hello_build

Create a Mix task at `mix/tasks/hello.ex`

    defmodule Mix.Tasks.Hello do
      use Mix.Task

      def run(param) do
        IO.puts("Hello #{param}")
      end
    end

Build archive

    mix archive.build

`hello_build-0.1.0.ez` file will be created in the project directory (.ez is zip archive)

Install archive

    mix archive.install hello_build-0.1.0.ez

Check if archive is installed

    mix archive
    ...
    * hello_build-0.1.0
    ...

Test archive

    mix hello World
    Hello World

Uninstall archive

    mix archive.uninstall hello_build-0.1.0

## mix.exs

### deps

Read more in [the official docs](https://hexdocs.pm/mix/1.13/Mix.Tasks.Deps.html)

Make the dependency available only in the given environment

    {:phoenix_live_reload, "~> 1.2", only: :dev},

Do not run the application

    {:credo, "~> 1.6", only: [:dev, :test], runtime: false}

Run the application only in the provided environment

    {:esbuild, "~> 0.3", runtime: Mix.env() == :dev}

## Dependency resoultion

Errors

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

Solution (add `override: true` for the package which is failed to use)

      {:ranch, "~> 1.7.1", , override: true}

## Resources

[Create a Mix Task for an Elixir Project](http://joeyates.info/2015/07/25/create-a-mix-task-for-an-elixir-project/)
