# Mix Tasks

Type for help

    ➜ mix ecto

Migrate database

    ➜ mix ecto.migrate

Drop database

    ➜ mix ecto.drop

## Aliases Defined in `mix.exs`

Setup database `"ecto.reset": ["ecto.drop", "ecto.setup"]`

    ➜ mix ecto.reset

Reset database `"ecto.setup": ["ecto.create", "ecto.migrate", "run priv/repo/seeds.exs"]`

    ➜ mix ecto.setup
