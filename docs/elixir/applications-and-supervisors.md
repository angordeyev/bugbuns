# Applications and Supervisors

## Application

An application is defined in `./mix.exs` file

```elixir
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
```

Then it is converted to `_build/dev/lib/example/ebin/example.app`

```erlang
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
```

The application module is `./lib/example/application.ex`

```elixir
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
```

## extra_applications

They are required to start applications which are part of Elixir ditribution. Another applications are started automatically.

## A simple starting module

Edit `mix.exs`

```elixir
def application do
  [
    mod: {HelloApp, []},
    ...
  ]
end
```

Create a module implementing `start/2`

```elixir
defmodule HelloApp do
  def start(_type, _args) do
    IO.puts "started"
    {:ok, self()} # pid should be returned
  end
end
```

`type` is :normal unless started in a distributed environment, it can have `:normal`, `:takeover`, `:failover` values in a distributed environment.
