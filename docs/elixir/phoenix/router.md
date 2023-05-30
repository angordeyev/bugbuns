## Phoenix Router

### Getting Routes

Show all routes from a terminal

    ➜ mix phx.routes

From iex

    iex> HelloRouterWeb.Router.Helpers.<Tab>

Path

    iex> HelloRouterWeb.Router.Helpers.user_path(HelloRouterWeb.Endpoint, :index)

`HelloRouterWeb.Router.Helpers` can be accessed like  `Routes` inside a test module
using `ConnCase`.

### Working with Router

Generate new project

    ➜ mix phx.new hello_router --no-ecto

Create Accounts context

    ➜ mix phx.gen.json Accounts User users name:string age:integer --no-context --no-schema

Add route

    scope "/api" do
      pipe_through :api

      get "/users", HelloRouterWeb.UserController, :index
    end

We can add namespace to the scope

    scope "/api", HelloRouterWeb do
      pipe_through :api

      get "/", UserController, :index
    end

Change user controller

    defmodule HelloRouterWeb.UserController do
      ...
      def index(conn, _params) do
        json(conn, [%{name: "John Doe", age: 20}])
      end
      ...
    end

Try curl

    ➜ curl http://localhost:4000/api/users
    [{"age":20,"name":"John Doe"}]

Change UserController namespace to

    defmodule HelloRouterWeb.Nested.UserController

Change router. See 'Nested' namespace is added.

    scope "/api", HelloRouterWeb do
      pipe_through :api

      scope "/nested", Nested do
        get "/users", UserController, :index
      end
    end

    ➜ curl http://localhost:4000/api/nested/users
    [{"age":20,"name":"John Doe"}]








