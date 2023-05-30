## Build

### Show warnings again

    mix compile --force # one command

    mix clean   # two commands
    mix compile

### Run mix applications

    mix # without console
    iex -S mix # with console

    mix phx.server # Phoenix without console
    iex -S mix phx.server # Phoenix with console

### Build structure

#### Simple application

    ➜ mix new hello_build
    ➜ mix compile
    ➜ tree _build/dev

    └── lib
        └── hello_build
            ├── consolidated
            │   ├── Elixir.Collectable.beam
            │   ├── Elixir.Enumerable.beam
            │   ├── Elixir.IEx.Info.beam
            │   ├── Elixir.Inspect.beam
            │   ├── Elixir.List.Chars.beam
            │   └── Elixir.String.Chars.beam
            └── ebin
                ├── Elixir.HelloBuild.beam
                └── hello_build.app

Add module

    defmodule NewModule do
      def hello do
        :world
      end
    end

Compile and see `Elixir.NewModule.beam` file is added

    ➜ mix compile
    ➜ tree _build/dev

    └── lib
        └── hello_build
            ...
            └── ebin
                ├── Elixir.HelloBuild.beam
                ├── Elixir.NewModule.beam
                └── hello_build.app

#### Phoenix application

    ➜ mix phx.new hello_phoenix_build
    ➜ mix compile
    ➜ tree _build/dev

    └── lib
        ....
        ├── hello_phoenix_build
        │   ├── consolidated
        │   │   ├── Elixir.Collectable.beam
        │   │   ...
        │   │   └── Elixir.Swoosh.Email.Recipient.beam
        │   ├── ebin
        │   │   ├── Elixir.HelloPhoenixBuild.Application.beam
        │   │   ├── Elixir.HelloPhoenixBuild.beam
        │   │   ├── Elixir.HelloPhoenixBuild.Mailer.beam
        │   │   ├── Elixir.HelloPhoenixBuild.Repo.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.Endpoint.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.ErrorHelpers.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.ErrorView.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.Gettext.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.LayoutView.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.PageController.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.PageView.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.Router.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.Router.Helpers.beam
        │   │   ├── Elixir.HelloPhoenixBuildWeb.Telemetry.beam
        │   │   └── hello_phoenix_build.app
        │   └── priv -> ../../../../priv
        ├── phoenix
        │   ├── ebin
        │   │   ├── Elixir.Mix.Phoenix.beam
        │   │   ....
        │   │   ├── Elixir.Plug.Exception.Phoenix.ActionClauseError.beam
        │   │   └── phoenix.app
        │   └── priv -> ../../../../deps/phoenix/priv
        │       └── telemetry_metrics.app
        ...
        └── telemetry_poller
            ├── ebin
            │   ├── telemetry_poller.app
            │   ...
            │   └── telemetry_poller_sup.beam
            └── mix.rebar.config
