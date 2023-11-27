# Associations

## Project

### Working with Associations

Generate a new project:

```shell
mix phx.new hello_assoc
```

Generate users:

```shell
mix phx.gen.context Blog Post posts text
mix phx.gen.context Blog Comment comments text post_id:references:posts
```

The migrations generated:

```elixir
# priv/repo/migrations/20220706195447_create_posts.exs
defmodule HelloAssoc.Repo.Migrations.CreatePosts do
  use Ecto.Migration

  def change do
    create table(:posts) do
      add :text, :string

      timestamps()
    end
  end
end
```

```elixir
# priv/repo/migrations/20220706195454_create_comments.exs
defmodule HelloAssoc.Repo.Migrations.CreateComments do
  use Ecto.Migration

  def change do
    create table(:comments) do
      add :text, :string
      add :post_id, references(:posts, on_delete: :nothing)

      timestamps()
    end

    create index(:comments, [:post_id])
  end
end
```

Schema files generated:

```elixir
# lib/hello_assoc/blog/post.ex
defmodule HelloAssoc.Blog.Post do
  ...
  schema "posts" do
    field :text, :string
    ...
  end
end
```

```elixir
# lib/hello_assoc/blog/comment.ex
defmodule HelloAssoc.Blog.Comment do
  ...
  schema "comments" do
    field :text, :string
    field :post_id, :id
    ...
  end
end
```

Possible associations are:

* has_many
* has_one
* belongs_to
* and more...

See the full list [Ecto Function](https://hexdocs.pm/ecto/Ecto.Schema.html#functions)

Let's play with queries.

Copy import and aliases from context to `.iex.exs`. It will alow to run quieries in iex with ease.

```elixir
defmodule HelloAssoc.Blog do
  ...
  import Ecto.Query, warn: false
  alias HelloAssoc.Repo

  alias HelloAssoc.Blog.Post
  ...
  alias HelloAssoc.Blog.Comment
  ...
end
```

Let's insert some data

```elixir
iex> Repo.insert!(%Post{
  text: "Hello",
  comments: [
    %Comment{text: "Excellent!"}
  ]
})
```
```output
** (KeyError) key :comments not found
(hello_assoc 0.1.0) expanding struct: HelloAssoc.Blog.Post.__struct__/1
iex:3: (file)
```

It does not work, let's add association to the "posts" schema.

```elixir
schema "posts" do
  ...
  has_many :comments, HelloAssoc.Blog.Comment
  ...
end
```

And execute again:

```elixir
iex> Repo.insert!(%Post{
  text: "Hello",
  comments: [
    %Comment{text: "Excellent!"}
  ]
})
```
```output
%HelloAssoc.Blog.Post{
  ...
}
```

Let's select posts:

```elixir
iex> Repo.all from p in Post
```
```output
[
  %HelloAssoc.Blog.Post{
    comments: #Ecto.Association.NotLoaded<association :comments is not loaded>,
    id: 1,
    ...
    text: "Hello",
    ...
  }
]
```

```elixir
iex> Repo.all from p in Post, preload: [:comments]
```
```output
[
  %HelloAssoc.Blog.Post{
    comments: [
      %HelloAssoc.Blog.Comment{
        ...
        id: 1,
        ...
        text: "Excellent!",
        ...
      }
    ],
    id: 1,
    ...
    text: "Hello",
    ...
  }
]
```

Let's select comments:

```elixir
iex> Repo.all from c in Comment
```
```output
[
  %HelloAssoc.Blog.Comment{
    ...
    id: 1,
    ...
    post_id: 1,
    text: "Excellent!",
    ...
  }
]
```

Let's replace `field :post_id, :id` with `belongs_to :post, HelloAssoc.Blog.Post` in `Comment` module.

```elixir
defmodule HelloAssoc.Blog.Comment do
  ...
  schema "comments" do
    ...
    belongs_to :post, HelloAssoc.Blog.Post
    ...
  end
end
```

Execute queries:

```elixir
iex> Repo.all from c in Comment
```
```output
[
  %HelloAssoc.Blog.Comment{
    ...
    id: 1,
    ...
    post: #Ecto.Association.NotLoaded<association :post is not loaded>,
    post_id: 1,
    text: "Excellent!",
    ...
  }
]
```


```elixir
iex> Repo.all from c in Comment, preload: [:post]
```
```output
[
  %HelloAssoc.Blog.Comment{
    ...
    id: 1,
    ...
    post: #Ecto.Association.NotLoaded<association :post is not loaded>,
    post_id: 1,
    text: "Excellent!",
    ...
  }
]

[
  %HelloAssoc.Blog.Comment{
    ...
    id: 1,
    ...
    post: %HelloAssoc.Blog.Post{
      ...
      comments: #Ecto.Association.NotLoaded<association :comments is not loaded>,
      id: 1,
      ...
      text: "Hello",
      ...
    },
    post_id: 1,
    text: "Excellent!",
    ...
  }
]
```

### Working with Embers

Let's work with embeds.

Generate the new migration

```shell
mix ecto.gen.migration embeds
```

Edit the migration:

```elixir
defmodule HelloAssoc.Repo.Migrations.Embeds do
  use Ecto.Migration

  def change do
    alter table(:posts) do
      add :links, :map
    end
  end
end
```

Create Link schema:

```elixir
defmodule HelloAssoc.Blog.Link do
  use Ecto.Schema

  embedded_schema do
    field :url
    timestamps
  end
end
```

Edit Post schema:

```elixir
defmodule HelloAssoc.Blog.Post do
  ...
  schema "posts" do
    ...
    embeds_many :links, HelloAssoc.Blog.Link
    ...
  end
  ...
end
```

Let's insert some data:

```elixir
Repo.insert!(%Post{
  text: "Hello",
  links: [
    %Link{url: "example.com/link1"},
    %Link{url: "example.com/link2"}
  ]
})
```

The link field in the database will contain the following content:

```elixir
[
  {
    "id": "c2506c3a-2101-4659-a3bd-878dc5312399",
    "url": "example.com/link1",
    "updated_at": "2022-09-01T09:59:49",
    "inserted_at": "2022-09-01T09:59:49"
  },
  {
    "id": "4018feb6-7fda-4e52-8509-26a3cf533e50",
    "url": "example.com/link2",
    "updated_at": "2022-09-01T09:59:49",
    "inserted_at": "2022-09-01T09:59:49"
  }
]
```

Let's select data:

```elixir
iex> Repo.all(Post)
```
```output
[
  ...
  %HelloAssoc.Blog.Post{
    ...
    id: 2,
    ...
    links: [
      %HelloAssoc.Blog.Link{
        id: "c2506c3a-2101-4659-a3bd-878dc5312399",
        inserted_at: ~N[2022-09-01 09:59:49],
        updated_at: ~N[2022-09-01 09:59:49],
        url: "example.com/link1"
      },
      %HelloAssoc.Blog.Link{
        id: "4018feb6-7fda-4e52-8509-26a3cf533e50",
        inserted_at: ~N[2022-09-01 09:59:49],
        updated_at: ~N[2022-09-01 09:59:49],
        url: "example.com/link2"
      }
    ],
    ...
  }
]
```

See more details for working with embeds [Embedded Schemas](https://hexdocs.pm/ecto/embedded-schemas.html)

## Resources

[Working with Ecto associations and embeds](https://dashbit.co/blog/working-with-ecto-associations-and-embeds)
