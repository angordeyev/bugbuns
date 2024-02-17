# Phoenix

## Configure

Generate a Phoenix application:

```shell
mix phx.new --install phoenix_release
```

Add release configuration to the project to generate unix files only:

```elixir title="mix.exs"
defmodule PhoenixRelease.MixProject do
  ...
  def project do
    ...
    phoenix_release: [
      include_executables_for: [:unix]
    ]
  end
  ...
end
```

Generate release files:

```shell
mix phx.gen.release
```

```output
* creating rel/overlays/bin/server
* creating rel/overlays/bin/server.bat
* creating rel/overlays/bin/migrate
* creating rel/overlays/bin/migrate.bat
* creating lib/phoenix_release/release.ex
```

You can delete files for unused platforms:

```shell
rm rel/overlays/bin/server.bat
rm rel/overlays/bin/migrate.bat
```
## Build

```shell
# Prepare static resources in priv/static
MIX_ENV=prod mix assets.deploy
```
```shell
MIX_ENV=prod mix release
```

## Run

Create a database:

```shell
sudo -u postgres psql -c 'create database phoenix_release;'
```

Generate secrets:

```shell
mix phx.gen.secret
```

Run:

```shell
SECRET_KEY_BASE=gK6UgeEmSWn3a9U46EMpwn07A8r4E8jFtZkPrxTyR+FFJP9VDgrARuW24uccyZge \
DATABASE_URL=ecto://postgres:postgres@localhost/phoenix_release \
_build/prod/rel/phoenix_release/bin/server
```

```shell
SECRET_KEY_BASE=gK6UgeEmSWn3a9U46EMpwn07A8r4E8jFtZkPrxTyR+FFJP9VDgrARuW24uccyZge \
DATABASE_URL=ecto://postgres:postgres@localhost/phoenix_release \
PHX_SERVER=true _build/prod/rel/phoenix_release/bin/phoenix_release start
```
## Resources

* [Mix Release Task. Mix Docs.](https://hexdocs.pm/mix/Mix.Tasks.Release.html)
* [Example: Running migrations in a release. Ecto SQL Docs.](https://hexdocs.pm/ecto_sql/Ecto.Migrator.html#module-example-running-migrations-in-a-release)
* [Example: Running migrations on application startup. Ecto SQL Docs.](https://hexdocs.pm/ecto_sql/Ecto.Migrator.html#module-example-running-migrations-on-application-startup)
* [Best way to run Migrations in Production. Sibelius Seraphini. Medium.](https://dev.to/woovi/best-way-to-run-migrations-in-production-ehg#:~:text=You%20should%20not%20run%20your,should%20be%20running%20the%20migration.)
