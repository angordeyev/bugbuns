# Configuration

## Configuration Files

The project configuration files are located in the `config` folder, the following files
are generate for a newly create Phoenix project:

  * `config.exs` - common configurateion file
  * `dev.exs` - dev environment configuration file
  * `prod.exs`- prod environment configuration file
  * `test.exs` - test environment configuration file
  * `runtime.exs` - runtime configuration

## Setting Configuration

Configs are done on the application scope

    config :hello_config,
      key1: "value1",
      key2: "value2"
      key3: [key31: "value31", key31: "value31"]
      key4: %{key41: "value41", key42: "value42"}

Config value can be overwritten

    config :hello_config,
      key2: "value_override",
      key5: "value5"

Config variable can be defined With root key

    config :hello_config, :root_key,
      key1: "value1",
      key2: "value2"

    config :hello_config, Some.Module,
      key1: "value1",
      key2: "value2"

Config with root key can have single value

    # preffered
    config :hello_config, :single_root_key, "single_root_value"

    # works, but not prefferred
    config :hello_config, single_root_key: "single_root_value"

`app_name` is the application name, then key-value pairs are listed using keyword list

    iex> Application.fetch_env!(:hello_config, :key1)
    value1

    iex> Application.fetch_env!(:hello_config, :root_key)
    [key1: "value1", key2: "value2"]

    iex> Application.fetch_env!(:hello_config, Some.Module)
    [key1: "value1", key2: "value2"]

    iex> Application.get_all_env(:hello_config)
    [
      ...
      {:key1, "value1"},
      {:key2, "value_override"},
      {:key3, [key31: "value31", key31: "value31"]},
      {:key4, %{key41: "value41", key42: "value42"}},
      {:key5, "value5"},
      {:root_key, [key1: "value1", key2: "value2"]}
      {Some.Module, [key1: "value1", key2: "value2"]},
      ...
    ]

    iex> Application.fetch_env!(:hello_config, :single_root_key)


So there is no config files in build files

Configuration files are compile time except config/runtime.exs

Put a line in `config/config.exs`

    IO.inspect(config_env(), label: "compile-time")

Compile the project

    ➜ mix compile
    compile-time: :dev

    ➜ MIX_ENV=test mix compile
    compile-time: :test

    ➜ mix phx.server
    compile-time: :dev # mix loads configuration from config/config.exs

Assemble release and run the project

    ➜ mix phx.gen.release
    ➜ mix release
    ➜ _build/dev/rel/hello_config/bin/server # no messages

Put a line in `config/config.exs`

    IO.inspect(config_env(), label: "runtime"

    ➜ mix compile
    compile-time: :dev

    ➜ _build/dev/rel/hello_config/bin/server
    runtime: :dev

Add to config

    config :hello_config,
      calculated: (IO.puts("calculating..."); 1 + 1)

    ➜ mix compile
    calculating...
    compile-time: :dev

Add to `start(_type, _args)` do

    IO.inspect(Application.fetch_env!(:hello_config, :calculated), label: "calculated")

    ➜ mix phx.server
    calculating...
    compile-time: :dev
    runtime: :dev
    calculated: 2

    ➜ mix phx.gen.release
    ➜ mix release
    ➜ _build/dev/rel/hello_config/bin/server
    runtime: :dev
    calculated: 2

**Checking the environment in runtime**

*Important*: `Mix` module is available when running an application using mix but
but is not available after building a release

config variable can be created

    config :hello_config, env: config_env()

And then checked

    if Application.fetch_env!(:hello_config, :env) == :dev do
      IO.puts("dev")
    end

But a better practice is to have configutation variable for the functionality in the corresponding
`dev.exs`, `prod.exs`, `test.exs` file.

    # dev.exs
    config :hello_config, connect_to_service: true

    # application file
    if Application.fetch_env!(:hel/lo_config, :connect_to_service) do
      Logger.info("Connecting to service...")
      ...
    end

### Resources

[Tips for Improving Your Elixir Configuration from core mainteiner of ElixirLS,
JASON AXELSON, ENGINEERING MANAGER THURSDAY, MARCH 31, 2022](https://felt.com/blog/elixir-configuration)


