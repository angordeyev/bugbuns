### Migrations

Migration are located in `priv/repo/migrations`

Generates a migration that a user can fill in with particular commands

    ➜ mix ecto.gen.migration <migration_name>

Migrate

    ➜ mix ecto.migrate

Create and alter table

    def change do
      create table(:devices) do # create -> alter to change
        add :name, :string
        add :age, :integer, :null: false # not null
        add :last_seen, :utc_datetime

        # creates automatically update inserted_at and updated_at fields
        timestamps(type: :utc_datetime)
      end
    end

Revert migration is generated automatically
