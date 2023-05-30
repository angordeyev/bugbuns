### Model View Controller

#### Html

##### Generation

Generate context

    ➜ mix phx.gen.html Users User users name:string
      mix ecto.migrate

Add the resource to the router `lib/hello_phoenix_web/router.ex`

    scope "/api", HelloPhoenixWeb do
      pipe_through :api

      resources "/users", UserController
    end

Files created

    lib/hello_phoenix/users.ex
    lib/hello_phoenix/users/user.ex

    lib/hello_phoenix_web/controllers/user_controller.ex

    lib/hello_phoenix_web/views/user_view.ex
    lib/hello_phoenix_web/templates/user/edit.html.heex
    lib/hello_phoenix_web/templates/user/form.html.heex
    lib/hello_phoenix_web/templates/user/index.html.heex
    lib/hello_phoenix_web/templates/user/new.html.heex
    lib/hello_phoenix_web/templates/user/show.html.heex

    test/hello_phoenix/users_test.exs
    test/hello_phoenix_web/controllers/user_controller_test.exs
    test/support/fixtures/users_fixtures.ex

    priv/repo/migrations/20220524105115_create_users.exs

#### Json

##### Generation

Generate context for json API

    ➜ mix phx.gen.json Communication Message messages text:string
      mix ecto.migrate

Add the resource to the router `lib/hello_phoenix_web/router.ex`

    scope "/api", HelloPhoenixWeb do
      pipe_through :api

      resources "/messages", MessageController, except: [:new, :edit]
    end

Files generated

    lib/hello_phoenix/communication.ex

    lib/hello_phoenix/communication/message.ex

    lib/hello_phoenix_web/controllers/message_controller.ex

    lib/hello_phoenix_web/views/message_view.ex

    test/hello_phoenix/communication_test.exs
    test/support/fixtures/communication_fixtures.ex
    test/hello_phoenix_web/controllers/message_controller_test.exs

    priv/repo/migrations/20220524105430_create_messages.exs

##### MVC

Let's get closer to MVC

Main context module contains functions to manipulate data

    defmodule HelloPhoenix.Communication do
      ...
      def list_messages do
        Repo.all(Message)
      end
      ...
      def get_message!(id), do: Repo.get!(Message, id)
      ...
      def delete_message(%Message{} = message) do
        Repo.delete(message)
      end
      ...
    end

Model contains data stucture and validation

    defmodule HelloPhoenix.Communication.Message do
      ...
      schema "messages" do
        field :text, :string

        timestamps()
      end

      def changeset(message, attrs) do
        message
        |> cast(attrs, [:text])
        |> validate_required([:text])
      end
    end

Controller

Let's look at the controller

    defmodule HelloEctoWeb.MessageController do
      use HelloEctoWeb, :controller
      ...
      action_fallback HelloEctoWeb.FallbackController

      def index(conn, _params) do
        messages = Communication.list_messages()
        Phoenix.Controller.render(conn, "index.json", messages: messages)
      end

      def create(conn, %{"message" => message_params}) do
        with {:ok, %Message{} = message} <- Communication.create_message(message_params) do
          conn
          |> put_status(:created)
          |> put_resp_header("location", Routes.message_path(conn, :show, message))
          |> render("show.json", message: message)
        end
      end
      ...
    end

`render` is `Phoenix.Controller.render/3` function, let's see how it works:

* it searches for the view with the same name, if the controller module is
  `HelloEctoWeb.MessageController` than it searches for the view model with
  the name `HelloEctoWeb.MessageView`. You can user other view using
  `Phoenix.Controller.put_view/2` ([see docs](https://hexdocs.pm/phoenix/Phoenix.Controller.html#put_view/2))
