# Phoenix Router

## Getting Routes

Show all routes from a terminal:

```shell
mix phx.routes
```

From IEx:

```elixir
iex> HelloRouterWeb.Router.Helpers.<Tab>
```

A path:

```elixir
iex> HelloRouterWeb.Router.Helpers.user_path(HelloRouterWeb.Endpoint, :index)
```

`HelloRouterWeb.Router.Helpers` can be accessed like  `Routes` inside a test module
using `ConnCase`.

## Working with Router

Generate a new project:

```shell
mix phx.new hello_router --no-ecto
```

Create Accounts context

```shell
mix phx.gen.json Accounts User users name:string age:integer --no-context --no-schema
```

Add a route:

```elixir
scope "/api" do
  pipe_through :api

  get "/users", HelloRouterWeb.UserController, :index
end
```

We can add a namespace to the scope:

```elixir
scope "/api", HelloRouterWeb do
  pipe_through :api

  get "/", UserController, :index
end
```

Change the user controller:

```elixir
defmodule HelloRouterWeb.UserController do
  ...
  def index(conn, _params) do
    json(conn, [%{name: "John Doe", age: 20}])
  end
  ...
end
```

Try curl:

```shell
curl http://localhost:4000/api/users
```
```output
[{"age":20,"name":"John Doe"}]
```

Change UserController namespace to:

```elixir
defmodule HelloRouterWeb.Nested.UserController
```

Change the router. See 'Nested' namespace is added:

```elixir
scope "/api", HelloRouterWeb do
  pipe_through :api

  scope "/nested", Nested do
    get "/users", UserController, :index
  end
end
```

```shell
curl http://localhost:4000/api/nested/users
```
```output
[{"age":20,"name":"John Doe"}]
```





