# Main Web Module

## Description

If the main module is named `SomeApplication` the main web module is named
`SomeApplicationWeb`.

## Using

    defmodule SomeApplicationWeb.Router do
      use SomeApplicationWeb, :router

<!---->

    defmodule SomeApplicationWeb.PageController do
      use SomeApplicationWeb, :controller

<!---->

    defmodule SomeApplicationWeb.PageView do
      use SomeApplicationWeb, :view

## Router Setup

    def router do
      quote do
        use Phoenix.Router

        import Plug.Conn
        import Phoenix.Controller
        import Phoenix.LiveView.Router
      end
    end

## Controller Setup

    def controller do
      quote do
        use Phoenix.Controller, namespace: SomeApplicationWeb

        import Plug.Conn
        import SomeApplicationWeb.Gettext
        alias SomeApplicationWeb.Router.Helpers, as: Routes
      end
    end


## View Setup

    def view do
      quote do
        use Phoenix.View,
          root: "lib/some_application_web/templates",
          namespace: SomeApplicationWeb

        # Import convenience functions from controllers
        import Phoenix.Controller,
          only: [get_flash: 1, get_flash: 2, view_module: 1, view_template: 1]

        # Include shared imports and aliases for views
        unquote(view_helpers())
      end
    end
