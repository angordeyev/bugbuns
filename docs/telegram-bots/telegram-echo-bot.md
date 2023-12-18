# Telegram Echo Bot

## Create Elixir Phoenix Project

If a bot does not exist create a new bot:

  1. Go to `@botfather`
  2. Enter `/newbot`
  3. Give the bot a name and a user name
  4. Copy the token

If a bot exists get the token:

  1. Go to `@botfather`
  2. Enter `/mybots`
  3. Select a bot
  4. Press "API Token" button
  5. Copy the token

Cteate a new project:

```shell
mix phx.new --no-ecto telegram_bot
```

Add `nadia` package to the dependencies:

```elixir title="mix.exs"
defmodule TelegramBot.MixProject do
  ...
  defp deps do
    [
      ...
      {:nadia, "~> 0.7.0"}
      ...
    ]
  end
  ...
end
```

Add the bot token to the config:

```elixir title="config/config.exs"
...
config :nadia, token: "<token>"

# Import environment specific config. This must remain at the bottom
# of this file so it overrides the configuration defined above.
import_config "#{config_env()}.exs"
```

Set the bot webhook:

https://api.telegram.org/bot{my_bot_token}/setWebhook?url={url_to_send_updates_to}


Add the webhook handler:

```elixir title="lib/telegram_bot_web/controllers/telegram_controller.ex"
defmodule TelegramBotWeb.TelegramController do
  use TelegramBotWeb, :controller

  def webhook(conn, params) do
    IO.inspect(params)
    json(conn, %{"status" => "ok"})
  end
end
```

```elixir title="lib/telegram_bot_web/router"
defmodule TelegramBotWeb.Router do
  use TelegramBotWeb, :router
  ...
  pipeline :api do
    plug :accepts, ["json"]
  end
  ...
  scope "/api", TelegramBotWeb do
    pipe_through :api
    post "/", TelegramController, :webhook
  end
  ...
end
```

## Deployment

Enter in the application folder and got through the following steps:

```shell
fly launch
```

Deploy:

```shell
fly deploy
```

## Resources

* [Marvin's Marvellous Guide to All Things Webhook. Telegram.](https://core.telegram.org/bots/webhooks)
