## Starting module

Simple starting module

Edit `mix.exs`

    def application do
      [
        mod: {HelloApp, []},
        ...
      ]
    end

Create module implementing `start/2`

    defmodule HelloApp do
      def start(_type, _args) do
        IO.puts "started"
        {:ok, self()} # pid should be returned
      end
    end

type is :normal unless started in a distributed environment, it can have :normal, :takeover :failover
values in a distributed environment.
