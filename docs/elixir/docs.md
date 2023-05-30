## Exdocs generation

Add to deps

    defp deps do
      [
        ...
        {:ex_doc, "~> 0.28.4"}
        ...
      ]
    end

Set project parameters

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

Generate documentation

    ➜ mix docs

Read help

    ➜ mix help docs

[ExDoc features documentation](https://hexdocs.pm/ex_doc/readme.html#features)
