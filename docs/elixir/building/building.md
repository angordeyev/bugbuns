# Building

## Tree Structure

Create a new Phoenix project:

```shell
mix phx.new phoenix_app --no-ecto --no-install
```

Get dependencies:

```shell
mix deps.get
```

It will create the files and directories:

```shell
_build
  dev
    lib
      phoenix_app
deps
  bandit
    ...
    lib
    ...
    mix.exs
    README.md
  ...
  phoenix
    ...
    lib
    ...
    mix.exs
    ...
    priv
      static
        favicon.ico
        ...
        phoenix.png
      templates
        phx.gen.auth
        phx.gen.context
        ...
  websock_adapter
mix.lock
```

Compile the project:

```shell
mix compile
```

The build is generated in `_build/dev/lib` folder:

```shell
phoenix_app
  consolidated
    Elixir.Bandit.HTTP2.Frame.Serializable.beam
    Elixir.Bandit.WebSocket.Frame.Serializable.beam
    Elixir.Bandit.WebSocket.Socket.beam
    Elixir.Collectable.beam
    Elixir.Enumerable.beam
    Elixir.IEx.Info.beam
    Elixir.Inspect.beam
    ...
  ebin
    Elixir.PhoenixApp.Application.beam
    Elixir.PhoenixApp.beam
    Elixir.PhoenixApp.Mailer.beam
    Elixir.PhoenixAppWeb.beam
    Elixir.PhoenixAppWeb.CoreComponents.beam
    Elixir.PhoenixAppWeb.Endpoint.beam
    ...
    phoenix_app.app
  priv
    gettext
      en
      errors.pot
    static
      favicon.ico
      images
      robots.txt
bandit
  ebin
    bandit.app
    Elixir.Bandit.Application.beam
    Elixir.Bandit.beam
    ...
    Elixir.Bandit.WebSocket.UpgradeValidation.beam
...
phoenix
  ebin
    Elixir.Mix.Phoenix.beam
    Elixir.Mix.Phoenix.Context.beam
    ...
    phoenix.app
  priv
    static
      favicon.ico
      ...
      phoenix.png
    templates
      phx.gen.auth
      phx.gen.context
        access_no_schema.ex
        context.ex
        ...
      ...
      phx.gen.socket
```

Generate a release:

```shell
mix release
```

The build is generated in `_build/dev/rel/phoenix_app` folder:

```shell
bin
  phoenix_app
  server
erts-14.0.2
  bin
    beam.smp
    ...
    erlc
    ...
    erl.src
    ...
    run_erl
lib
  ...
  bandit-1.2.2
  ...
  phoenix-1.7.11
  ...
releases
  0.1.0
    consolidated
    elixir
    env.sh
    iex
    phoenix_app.rel
    remote.vm.args
    runtime.exs
    start.boot
    start_clean.boot
    start_clean.script
    start.script
    sys.config
    vm.args
  COOKIE
  start_erl.data
```
