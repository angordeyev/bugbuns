## Simple Service

Generate the application

    ➜ mix phx.new simple_service \
      --no-ecto --no-html --no-assets --no-dashboard --no-gettext --no-mailer --no-live

Generate Controller

    ➜ mix phx.gen.json Communication Message messages text:string --no-context --no-schema

Add get request to the router

    scope "/api", SimpleServiceWeb do
      pipe_through :api
      get "/messages", MessageController, :index
    end

Edit controller

    defmodule SimpleServiceWeb.MessageController do
      ....
      def index(conn, _params) do
        IO.inspect(conn.req_headers, label: "headers")
        conn = put_resp_header(conn, "Key", "Value")
        json(conn, "{}")
      end
      ...
    end

Run the service

    ➜ iex -S mix phx.server

Try with curl

    ➜ curl http://localhost:4000/api/messages -H "Key: Value"

See `curl` output, response header "Key" case is preserved, however it
is standard to use lower-kebab-case for response headers.

    HTTP/1.1 200 OK
    Key: Value
    cache-control: max-age=0, private, must-revalidate
    content-length: 4
    content-type: application/json; charset=utf-8
    date: Tue, 12 Jul 2022 17:30:50 GMT
    server: Cowboy
    x-request-id: FwElNelfTtl5Z1EAAAHB

See `IO.inspect` output, Header key is trasformed to lower case ("Key" -> "key")
but value is letter cases are preserved ("Value").

    headers: [
      {"accept", "*/*"},
      {"host", "localhost:4000"},
      {"key", "Value"},
      {"user-agent", "curl/7.84.0"}
    ]
