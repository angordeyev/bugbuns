## Phoenixs

### Creating Application

Create application

    mix phx.new hello_phoenix

Context are modules with releated functionality.
For examples a group of modules related to user functionality:

HelloPhoenix.Users - context
HelloPhoenix.Users.User - model
HelloPhoenixWeb.UserController - controller
HelloPhoenixWeb.UserView - view

Generate controller, views, and context for an HTML resource

There can be multiple models in one context. One context for multiple models may be user to combine
closely related functionality.

    mix phx.gen.html Users User users name:string
    mix setup

Create `/api` scope section and resource to `HelloUsersWeb.Router` in `router.ex`

    scope "/api", HelloPhoenixWeb do
      pipe_through :api

      resources "/users", UserController
    end

Show all routes

    mix phx.routes

The following paths are available:

    GET     /users          :index    show all the users
    GET     /users/:id      :show     show a user identified by id slug[^1]

    GET     /users/new      :new      show a form for creating a new user
    GET     /users/:id/edit :edit     get a user by id and show a form for editing

    POST    /users          :create   save a new user
    PUT     /users/:id      :update   update the user with an id using full object to replace
    PATCH   /users/:id      :update   update the user with an id using parial information
                                      (field-value pairs or change instructions)

    DELETE  /users/:id      :delete   remove the user with an id

You can go to `http://localhost:4000/users` and play with listing, creating, and updating users

Generates controller, views, and context for a JSON resource

    mix phx.gen.json Communication Message messages text:string
    mix ecto.migrate

Add resource to `HelloUsersWeb.Router` in `router.ex`

    scope "/api", HelloPhoenixWeb do
      pipe_through :api

      resources "/users", UserController
      resources "/messages", MessageController, except: [:new, :edit]
    end

### Working with curl

Insert new message

    ➜ curl -i -X POST localhost:4000/api/messages --header "Content-Type: application/json" \
       -d '{"message": {"text": "hello world"}}'

    201 Created
    {
      "data": {
        "id": 1,
        "text": "hello world
      }
    }

    ➜ curl -i -X POST localhost:4000/api/messages --header "Content-Type: application/json" \
       -d '{"message": {}}'

    422 Unprocessable Entity
    {
      "errors":{
        "text":["can't be blank"]
      }
    }

Get message

    ➜ curl -i -X GET localhost:4000/api/messages/1
    200 OK
    {
      "data": {
        "id": 1,
        "text": "hello world
      }
    }

    curl -i -X GET localhost:4000/api/messages/1000000
    404 Not Found
    ....

Update message

    ➜ curl -i -X PUT localhost:4000/api/messages/1 --header "Content-Type: application/json" \
       -d '{"message": {"text": "hello world 1"}}'

    200 OK
    {
      "data":{
        "id": 1,
        "text": "hello world 1"
      }
    }

    ➜ curl -i -X PATCH localhost:4000/api/messages/1 --header "Content-Type: application/json" \
       -d '{"message": {"text": "hello world 1"}}'

    200 OK
    {
      "data":{
        "id":4,
        "text":"hello world 1"
      }
    }

    ➜ curl -i -X GET localhost:4000/api/messages/1

    200 OK
    {
      "data":{
        "id":1,
        "text":"hello world 1"
      }
    }

Delete message

    ➜ curl -i -X DELETE localhost:4000/api/messages/1

    204 No Content

    # 204 means that the content no longer exist but the client does not need to
    # navigate away from the page

Insert more messages

    ➜ curl -X POST localhost:4000/api/messages --header "Content-Type: application/json" \
      -d '{"message": {"text": "hello world"}}'

    {"data":{"id":2,"text":"hello world"}}

    ➜ curl -X POST localhost:4000/api/messages --header "Content-Type: application/json" \
      -d '{"message": {"text": "hello world"}}'

    {"data":{"id":2,"text":"hello world"}}

List messages

    ➜ curl -i -X GET localhost:4000/api/messages

    HTTP/1.1 200 OK
    {
      "data":
      [
        {"id":2,"text":"hello world"},
        {"id":3,"text":"hello world"}
      ]
    }

### Working with HTTPoision

#### List

    iex> (HTTPoison.post! "localhost:4000/api/messages",
          Jason.encode!(%{message: %{text: "some_text"}}),
          [{"Content-Type", "application/json"}])

    %HTTPoison.Response{
      body: "{\"data\":{\"id\":19,\"text\":\"some_text\"}}",
      headers: [
        {"cache-control", "max-age=0, private, must-revalidate"},
        {"content-length", "37"},
        {"content-type", "application/json; charset=utf-8"},
        {"date", "Sat, 04 Jun 2022 06:25:40 GMT"},
        {"location", "/messages/19"},
        {"server", "Cowboy"},
        {"x-request-id", "FvVW3A5jzPK8M_sAAACk"}
      ],
      request: %HTTPoison.Request{
        body: "{\"message\":{\"text\":\"some_text\"}}",
        headers: [{"Content-Type", "application/json"}],
        method: :post,
        options: [],
        params: %{},
        url: "http://localhost:4000/api/messages"
      },
      request_url: "http://localhost:4000/api/messages",
      status_code: 201
    }

See the status code is 201 and response "location" is "/messages/19",
so the browser will redirect to that page

#### Delete

    iex> HTTPoison.delete! "localhost:4000/api/messages/7"
    %HTTPoison.Response{
      body: "",
      headers: [
        {"cache-control", "max-age=0, private, must-revalidate"},
        {"date", "Sat, 04 Jun 2022 06:45:01 GMT"},
        {"server", "Cowboy"},
        {"x-request-id", "FvVX6kggC-OBkLkAAAAi"}
      ],
      request: %HTTPoison.Request{
        body: "",
        headers: [],
        method: :delete,
        options: [],
        params: %{},
        url: "http://localhost:4000/api/messages/7"
      },
      request_url: "http://localhost:4000/api/messages/7",
      status_code: 204
    }

## Phoenix generators

**Messages**

`mix phx.gen.context Messages Message messages text:string`

Context:          lib/hello_phx_generation/messages.ex

Data model:       lib/hello_phx_generation/messages/message.ex
Migration:        priv/repo/migrations/20220521112614_create_messages.exs

Context tests:    test/hello_phx_generation/messages_test.exs
Context fuxtures: test/support/fixtures/messages_fixtures.ex

There may be multiple modules in one context

**Users**

Context:           lib/application/users1.ex
DataModel:         lib/application/users1/user2.ex
Migration:         priv/repo/migrations/20220521105605_create_users3.exs

Context tests:    test/application/users1_test.exs
Context fixtures: test/support/fixtures/users1_fixtures.ex

Adding:

Controller:      lib/application_web/controllers/user2_controller.ex
View:            lib/application_web/views/user2_view.ex

Controller test: test/application_web/controllers/user2_controller_test.exs

Common:

Fallback controller: lib/application_web/controllers/fallback_controller.ex
Changeser error view: lib/application_web/views/changeset_view.ex


**Devices**

DataModel:  lib/application/devices1/device2.ex
View:       lib/application_web/views/device2_view.ex
Controller: lib/application_web/controllers/device2_controller.ex



priv/repo/migrations/20220521110019_create_devices3.exs

lib/application/devices1.ex

test/application_web/controllers/device2_controller_test.exs
test/application/devices1_test.exs
test/support/fixtures/devices1_fixtures.ex

**Phoenix Project Structure**

Assets:

├── assets
│   ├── css
│   │   ├── app.css
│   │   └── phoenix.css
│   ├── js
│   │   └── app.js
│   └── vendor
│       └── topbar.js
├── config
│   ├── config.exs
│   ├── dev.exs
│   ├── prod.exs
│   ├── runtime.exs
│   └── test.exs



├── lib
│   ├── hello_phx_generation.ex
│   ├── hello_phx_generation
│   │   ├── application.ex
│   │   ├── mailer.ex
│   │   ├── messages.ex
│   │   ├── repo.ex
│   │   ├── messages
│   │   │   └── message.ex
│   └── hello_phx_generation_web.ex
│   ├── hello_phx_generation_web
│   │   ├── controllers
│   │   │   ├── device2_controller.ex
│   │   │   ├── fallback_controller.ex
│   │   │   ├── page_controller.ex
│   │   │   ├── phone2_controller.ex
│   │   │   └── user2_controller.ex
│   │   ├── endpoint.ex
│   │   ├── gettext.ex
│   │   ├── router.ex
│   │   ├── telemetry.ex
│   │   ├── templates
│   │   │   ├── layout
│   │   │   │   ├── app.html.heex
│   │   │   │   ├── live.html.heex
│   │   │   │   └── root.html.heex
│   │   │   └── page
│   │   │       └── index.html.heex
│   │   └── views
│   │       ├── changeset_view.ex
│   │       ├── device2_view.ex
│   │       ├── error_helpers.ex
│   │       ├── error_view.ex
│   │       ├── layout_view.ex
│   │       ├── page_view.ex
│   │       ├── phone2_view.ex
│   │       └── user2_view.ex
├── mix.exs
├── mix.lock

├── priv
│   ├── gettext
│   │   ├── en
│   │   │   └── LC_MESSAGES
│   │   │       └── errors.po
│   │   └── errors.pot
│   ├── repo
│   │   ├── migrations
│   │   │   ├── 20220521105605_create_users3.exs
│   │   │   ├── 20220521110019_create_devices3.exs
│   │   │   ├── 20220521112614_create_messages.exs
│   │   │   ├── 20220521113014_create_messages.exs
│   │   │   ├── 20220521113100_create_messages.exs
│   │   │   ├── 20220521113153_create_messages.exs
│   │   │   ├── 20220521113220_create_messages.exs
│   │   │   └── 20220521163742_create_phone3.exs
│   │   └── seeds.exs
│   └── static
│       ├── assets
│       │   ├── app.css
│       │   └── app.js
│       ├── favicon.ico
│       ├── images
│       │   └── phoenix.png
│       └── robots.txt
├── README.md

Tests:

└── test
    ├── hello_phx_generation
    │   ├── devices1_test.exs
    │   ├── messages_test.exs
    │   └── users1_test.exs
    ├── hello_phx_generation_web
    │   ├── channels
    │   ├── controllers
    │   │   ├── device2_controller_test.exs
    │   │   ├── page_controller_test.exs
    │   │   ├── phone2_controller_test.exs
    │   │   └── user2_controller_test.exs
    │   └── views
    │       ├── error_view_test.exs
    │       ├── layout_view_test.exs
    │       └── page_view_test.exs
    ├── support
    │   ├── channel_case.ex
    │   ├── conn_case.ex
    │   ├── data_case.ex
    │   └── fixtures
    │       ├── devices1_fixtures.ex
    │       ├── messages_fixtures.ex
    │       └── users1_fixtures.ex
    └── test_helper.exs

## Authentication

[A deep dive into authentication in Elixir Phoenix with phx.gen.auth](https://levelup.gitconnected.com/a-deep-dive-into-authentication-in-elixir-phoenix-with-phx-gen-auth-9686afecf8bd)

## Phoenix naming convension

Tests should end with `test` postfix

## Phoenix PubSub

## Resources

[^1]: Slug - unique identifier in a web address after the last backslash
      Происхождение: В типографии использовались для идентификации статей,
      ранее металлический штамм строки, набранный из букв


