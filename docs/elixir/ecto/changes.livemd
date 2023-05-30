# Changes

```elixir
Mix.install([:ecto])
ExUnit.start()
```

## Schema

```elixir
defmodule HelloEcto.Communication.Message do
  use Ecto.Schema
  import Ecto.Changeset

  schema "messages" do
    field(:tag, :string)
    field(:text, :string)

    timestamps()
  end

  @doc false
  def changeset(message, attrs) do
    message
    |> cast(attrs, [:text, :tag])
    |> validate_required([:text, :tag])
  end
end
```

```elixir
alias HelloEcto.Communication.Message
```

## Changesets

```elixir
cs = Message.changeset(%Message{}, %{text: "some_text", tag: "some_tag"})
```

Changeset is a struct, let's see it's structure

```elixir
IEx.Helpers.i(cs)
```

Empty changeset

```elixir
%Ecto.Changeset{}
```

Changeset workd with schemas and `{data, types}` structure

```elixir
cs = Ecto.Changeset.change(%Message{text: "old"}, %{text: "new"})
[cs, cs.data]
```

```elixir
Ecto.Changeset.change({%{text: "old"}, %{text: :string}}, %{text: "new"})
```

## No changes

```elixir
Ecto.Changeset.change({%{text: "same"}, %{text: :string}}, %{text: "same"})
```

## Cast

```elixir
Ecto.Changeset.change(%Message{text: "old"}, %{text: "new"})
```

Cast has field list parameter

```elixir
Ecto.Changeset.cast(%Message{text: "old"}, %{text: "new"}, [:text])
```

It the field list is empty no changes will be generated

```elixir
Ecto.Changeset.cast(%Message{text: "old"}, %{text: "new"}, [])
```

```elixir
[
  Ecto.Changeset.change(%Message{text: "old"}, %{text: "new", tag: "urgent"}),
  # cast will generate only selected fields changes
  Ecto.Changeset.cast(%Message{text: "old"}, %{text: "new", tag: "urgent"}, [:text])
]
```

```elixir
defmodule SomeTest do
  use ExUnit.Case

  test "Exception is raised for unknown field 'status' during change" do
    assert_raise ArgumentError,
                 fn -> Ecto.Changeset.change(%Message{text: "old"}, %{text: "new", status: 1}) end
  end

  test "Status field is skipped during cast" do
    # status field is skipped
    Ecto.Changeset.cast(%Message{text: "old"}, %{text: "new", status: 1}, [:text])
  end

  test "Exception is raised for unknown field 'status' during cast" do
    assert_raise ArgumentError,
                 fn ->
                   Ecto.Changeset.cast(%Message{text: "old"}, %{text: "new", status: 1}, [
                     :text,
                     :status
                   ])
                 end
  end
end

ExUnit.run()
```

## Partial and full update

[Validate required for a partial update](https://github.com/elixir-ecto/ecto/issues/2814)

```elixir
Message.changeset(%Message{}, %{text: "hello"})
```

## Update using query

```elixir
HelloEcto.Users.list_users()
```

```elixir
# Update
{count, nil} =
  from(a in AppUser, where: a.email == ^email)
  |> Repo.update_all(
    set: [
      password_reset_token: password_reset_token,
      password_reset_sent_at: password_reset_sent_at
    ]
  )
```
