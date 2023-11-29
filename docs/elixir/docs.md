# ExDoc generation

Add to deps:

```elixir
defp deps do
  [
    ...
    {:ex_doc, "~> 0.28.4"}
    ...
  ]
end
```

Set the project parameters:

```elixir
def project do
  [
    ...
    # Docs
    name: "MyApp",
    source_url: "https://github.com/USER/PROJECT",
    homepage_url: "http://YOUR_PROJECT_HOMEPAGE",
    docs: [
      main: "readme", # The main page in the docs
      #logo: "path/to/logo.png",
      extras: ["README.md"]
    ]
    ...
  ]
end
```

Generate the documentation:

```shell
mix docs
```

Read help:

```shell
mix help docs
```

[ExDoc features documentation](https://hexdocs.pm/ex_doc/readme.html#features)
