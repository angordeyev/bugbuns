# Assets Management

## Esbuild Setup

In `mix.exs`

    defp deps do
      ...
      {:esbuild, "~> 0.5", runtime: Mix.env() == :dev},
      ...
    end

    defp aliases do
      ...
      "assets.deploy": ["esbuild default --minify", "phx.digest"]
      ...
    end

In `config/config.exs`

    config :esbuild,
      version: "0.14.41",
      default: [
        args: ~w(js/app.js --bundle --target=es2016 --outdir=../priv/static/assets
          --external:/fonts/* --external:/images/*),
        cd: Path.expand("../assets", __DIR__),
        env: %{"NODE_PATH" => Path.expand("../deps", __DIR__)}
      ]

In `dev.exs`

    config :some_app, SomeAppWeb.Endpoint,
      ...
      watchers: [
        ...
        # Start the esbuild watcher by calling Esbuild.install_and_run(:default, args)
        esbuild: {Esbuild, :install_and_run, [:default, ~w(--sourcemap=inline --watch)]}
        ...
      ]

Import `app.css` to `assets/js/app.js` to bundle css

    import "../css/app.css"


