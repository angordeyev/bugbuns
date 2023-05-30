## Ecto

ecto - outside, external, shell for ineracting with external database

### Generating simple project

Generate new project

    ➜ mix phx.new hello_ecto

The Repo code will be generated

Repo application will be added to supervisor

    # lib/hello_ecto/application.ex
    defmodule HelloEcto.Application do
      def start(_type, _args) do
        children = [
          ...
          HelloEcto.Repo,
          ...
        ]
    end

Repo module

    # lib/hello_ecto/repo.ex
    defmodule HelloEcto.Repo do
      use Ecto.Repo,
        otp_app: :hello_ecto,
        adapter: Ecto.Adapters.Postgres
    end

Configs

    # config/config.exs
    ...
    config :hello_ecto,
      ecto_repos: [HelloEcto.Repo]
    ...

    # config/dev.exs
    ...
    config :hello_ecto, HelloEcto.Repo,
      username: "postgres",
      password: "postgres",
      hostname: "localhost",
      database: "hello_ecto_dev",
      show_sensitive_data_on_connection_error: true,
      pool_size: 10
    ...


    # config/runtime.exs
    ...
    if config_env() == :prod do
      database_url =
        System.get_env("DATABASE_URL") ||
      ...
      config :hello_ecto, HelloEcto.Repo,
        ...
        url: database_url,
        pool_size: String.to_integer(System.get_env("POOL_SIZE") || "10"),
        socket_options: maybe_ipv6
    ...

Create the database

    ➜ mix ecto.setup

Reset database

    ➜ mix ecto.drop && mix ecto.drop

Generate the context (see Phoenix context)

    ➜ mix phx.gen.json Communication Message messages text:string

Then try to select data

    iex> HelloEcto.Repo.all(HelloEcto.Communication.Message)

You can create `.iex.exs` file for convenince with the following content:

    alias HelloEcto.Repo

Then you can query like

    iex> Repo.all(HelloEcto.Communication.Message)

    # Show the query and retuns emtpy collection as we have not added any message entries
    [debug] QUERY OK source="messages" db=0.7ms decode=1.3ms queue=0.6ms idle=4.0ms
    SELECT m0."id", m0."text", m0."inserted_at", m0."updated_at" FROM "messages" AS m0 []
    []

For raw sql

    # Same as Repo.query("SELECT * FROM messages)
    iex> Repo.query "SELECT text FROM messages"

    [debug] QUERY OK db=0.7ms queue=0.8ms idle=1537.8ms
    SELECT text FROM messages []
    {:ok,
     %Postgrex.Result{
       columns: ["text"],
       command: :select,
       connection_id: 23188,
       messages: [],
       num_rows: 0,
       rows: []
     }}

Let's insert something

    iex> Repo.insert(%HelloEcto.Communication.Message{text: "first message"})

    [debug] QUERY OK db=3.1ms decode=1.7ms queue=0.7ms idle=1008.5ms
    INSERT INTO "messages" ("text","inserted_at","updated_at") VALUES ($1,$2,$3) RETURNING "id" ["first message", ~N[2022-06-02 11:19:03], ~N[2022-06-02 11:19:03]]
    {:ok,
     %HelloEcto.Communication.Message{
       __meta__: #Ecto.Schema.Metadata<:loaded, "messages">,
       id: 1,
       inserted_at: ~N[2022-06-02 11:19:03],
       text: "first message",
       updated_at: ~N[2022-06-02 11:19:03]
     }}

And see the inserted message

    iex> message = Repo.get(HelloEcto.Communication.Message, 1) # get by id

    [debug] QUERY OK source="messages" db=0.7ms queue=1.1ms idle=1427.9ms
    SELECT m0."id", m0."text", m0."inserted_at", m0."updated_at" FROM "messages" AS m0 WHERE (m0."id" = $1) [1]
    %HelloEcto.Communication.Message{
      __meta__: #Ecto.Schema.Metadata<:loaded, "messages">,
      id: 1,
      inserted_at: ~N[2022-06-02 11:19:03],
      text: "first message",
      updated_at: ~N[2022-06-02 11:19:03]
    }

Delete the message

    iex> Repo.delete(message)

    [debug] QUERY OK db=1.2ms queue=0.6ms idle=1428.6ms
    DELETE FROM "messages" WHERE "id" = $1 [1]
    {:ok,
     %HelloEcto.Communication.Message{
       __meta__: #Ecto.Schema.Metadata<:deleted, "messages">,
       id: 1,
       inserted_at: ~N[2022-06-02 11:19:03],
       text: "first message",
       updated_at: ~N[2022-06-02 11:19:03]
     }}


Let's add alias to `.iex.exs`

    alias HelloEcto.Communication.Messages

Create repository, so you can see changes after adding new field using codegeneration.

    git init

Add field

    ➜ mix phx.gen.json Communication Message messages text:string tag:string

Delete generated migration, we can see changes using `git status`

Add new migration and add "tag" field

    ➜ mix ecto.gen.migration message_add_tag

    defmodule HelloEcto.Repo.Migrations.MessageAddTag do
      ...
      def change do
        alter table(:messages) do
          add :tag, :string
        end
      end
    end

    ➜ mix ecto.migrate

### Working with Ecto.Changeset

Changeset function looks like

    # lib/hello_ecto/communication/message.ex
    def changeset(message, attrs) do
      message
      |> cast(attrs, [:text, :tag])
      |> validate_required([:text, :tag])
    end

Generate changeset

    iex> Message.changeset(%Message{}, %{text: "some_text", tag: "some_tag"})
    #Ecto.Changeset<
      action: nil,
      changes: %{tag: "some_tag", text: "some_text"},
      errors: [],
      data: #HelloEcto.Communication.Message<>,
      valid?: true
    >

Changeset is struct, it just implements own inspect format for IO.inspect using "#Ecto.Changeset<>" format

    iex> i cs

    Term
      #Ecto.Changeset<action: nil, changes: %{tag: "some_tag", text: "some_text"}, errors: [], data: #HelloEcto.Communication.Message<>, valid?: true>
    Data type
      Ecto.Changeset
    Description
      This is a struct. Structs are maps with a __struct__ key.
    Reference modules
      Ecto.Changeset, Map
    Implemented protocols
      IEx.Info, Inspect, Jason.Encoder, Phoenix.HTML.FormData, Phoenix.Param, Plug.Exception, Swoosh.Email.Recipient

Let's create empty changeset

    iex> %Ecto.Changeset{}
    #Ecto.Changeset<action: nil, changes: %{}, errors: [], data: nil, valid?: false>

Changeset works with schemas and `{data, types}` structure

    iex> cs = Ecto.Changeset.change(%Message{text: "old"}, %{text: "new"})
    #Ecto.Changeset<
      action: nil,
      changes: %{text: "new"},
      errors: [],
      data: #HelloEcto.Communication.Message<>,
      valid?: true
    >

    iex> Ecto.Changeset.change(%Message{text: "old"}, %{text: 1})
    # no erors, fild type is not checked, use cast for type check
    #Ecto.Changeset<
      action: nil,
      changes: %{text: 1},
      errors: [],
      data: #HelloEcto.Communication.Message<>,
      valid?: true
    >

    iex> cs.data
    %HelloEcto.Communication.Message{
      __meta__: #Ecto.Schema.Metadata<:built, "messages">,
      id: nil,
      inserted_at: nil,
      tag: nil,
      text: "old",
      updated_at: nil
    }

    iex> Ecto.Changeset.change({%{text: "old"}, %{text: :string}}, %{text: "new"})
    #Ecto.Changeset<
      action: nil,
      changes: %{text: "new"},
      errors: [],
      data: %{text: "old"},
      valid?: true
    >

    Ecto.Changeset.change({%{text: "same"}, %{text: :string}}, %{text: "same"})

    #Ecto.Changeset<
      action: nil,
      changes: %{},
      errors: [],
      data: %{text: "same"},
      valid?: true
    >

Cast

    iex> Ecto.Changeset.change(%Message{text: "old"}, %{text: "new"})
    #Ecto.Changeset<
      action: nil,
      changes: %{text: "new"},
      errors: [],
      data: #HelloEcto.Communication.Message<>,
      valid?: true
    >

    Ecto.Changeset.cast(%Message{text: "old"}, %{text: "new"}, [:text])
    #Ecto.Changeset<
      action: nil,
      changes: %{text: "new"},
      errors: [],
      data: #HelloEcto.Communication.Message<>,
      valid?: true
    >

    Ecto.Changeset.cast(%Message{text: "old"}, %{text: 1}, [:text])
    # Type is checked
    #Ecto.Changeset<
      action: nil,
      changes: %{},
      errors: [text: {"is invalid", [type: :string, validation: :cast]}],
      data: #HelloEcto.Communication.Message<>,
      valid?: false
    >

    Ecto.Changeset.cast(%Message{text: "old"}, %{text: "new", tag: 1}, [:text])
    # Only "text" field is checked to match type
    #Ecto.Changeset<
      action: nil,
      changes: %{text: "new"},
      errors: [],
      data: #HelloEcto.Communication.Message<>,
      valid?: true
    >

Insert changeset to repo

    iex> cs = Ecto.Changeset.change(%Message{}, %{text: "new"})
    iex> Repo.insert(cs)
    # The Message is returned after the successful operation
    {:ok,
     %HelloEcto.Communication.Message{
       __meta__: #Ecto.Schema.Metadata<:loaded, "messages">,
       id: 4,
       inserted_at: ~N[2022-06-03 17:55:09],
       tag: nil,
       text: "new",
       updated_at: ~N[2022-06-03 17:55:09]
     }}

    iex> Repo.all(Message)

    [debug] QUERY OK source="messages" db=0.7ms queue=0.9ms idle=1847.4ms
    SELECT m0."id", m0."tag", m0."text", m0."inserted_at", m0."updated_at" FROM "messages" AS m0 []
    [
      %HelloEcto.Communication.Message{
        __meta__: #Ecto.Schema.Metadata<:loaded, "messages">,
        id: 1,
        inserted_at: ~N[2022-06-03 17:12:14],
        tag: nil,
        text: "new",
        updated_at: ~N[2022-06-03 17:12:14]
      }
    ]

Validate required

    iex> cs = \
      %Message{} \
      |> Ecto.Changeset.cast(%{text: "new"}, [:text, :tag]) \
      |> Ecto.Changeset.validate_required([:text, :tag])

    #Ecto.Changeset<
      action: nil,
      changes: %{text: "new"},
      errors: [tag: {"can't be blank", [validation: :required]}],
      data: #HelloEcto.Communication.Message<>,
      valid?: false
    >

    iex> Repo.insert(cs)

    # see the :insert action is added to changeset
    {:error,
     #Ecto.Changeset<
       action: :insert,
       changes: %{text: "new"},
       errors: [tag: {"can't be blank", [validation: :required]}],
       data: #HelloEcto.Communication.Message<>,
       valid?: false
     >}

### Working without schema

Crete new migration

    ➜ mix ecto.gen.migration documents

Edit migration

    defmodule HelloEcto.Repo.Migrations.Documents do
      ...
      def change do
        create table(:document) do
          add :text, :string
          add :tag, :string

          timestamps()
        end
      end
    end

Migrate

    ➜ mix ecto.migrate

Import `Ecto.Query` in `.iex.exs`

    import Ecto.Query

Try select query

    iex> Repo.all from "document", select: [:id, :text, :tag]

### Extending Repo module

    def count(table) do
     HelloEcto.Repo.aggregate(table, :count, :id)
    end

    iex> Repo.count(Message)

    [debug] QUERY OK source="messages" db=0.8ms decode=1.7ms queue=1.0ms idle=593.6ms
    SELECT count(m0."id") FROM "messages" AS m0 []
    0
