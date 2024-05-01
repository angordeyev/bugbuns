---
draft: true
---

# libcluster

```shell
mix phx.new with_libcluster --no-ecto --no-gettext --no-mailer --no-assets --no-html
```

Add to `config/runtime.exs`:

```elixir
if config_env() == :dev do
  port = String.to_integer(System.get_env("PORT") || "4000")

  config :with_libcluster, WithLibclusterWeb.Endpoint,
    http: [
      port: port
    ]
end
```

Run nodes in different terminals:

```shell
PORT=4001 iex --sname a -S mix phx.server
```

```shell
PORT=4002 iex --sname b -S mix phx.server
```

```shell
PORT=4003 iex --sname c -S mix phx.server
```

On node A:

```elixir
Node.list()
```

```output
[:b@angarch, :c@angarch]
```

On node B:

```elixir
Node.list()
```

```output
[:a@angarch, :c@angarch]
```

## Resources

* [Connecting Elixir Nodes with libcluster, locally and on Kubernetes. Alvise Susmel.](https://www.poeticoding.com/connecting-elixir-nodes-with-libcluster-locally-and-on-kubernetes/)

