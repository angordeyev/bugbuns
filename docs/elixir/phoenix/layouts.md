# Layouts

Common layout pages

## The New Phoenix Project Generated Layouts

Generate new project

```shell
mix phx.new hello_layouts
mix ecto.setup
```

Generate live page and add the generated pages to the router

```shell
mix phx.gen.live Messages Message messages text:string
```

See the folder `lib/hello_layouts_web/templates/layout`.
The following files are generated:

  * root.html.heex - layout for all pages
  * app.html.heex  - inner layout for normal pages
  * live.html.heex - inner layout for live pages

```html title="root.html.heex"
<!DOCTYPE html>
<html lang="en">
  <head>
   ...
  </head>
  <body>
    <header>
    ...
    </header>
    <%= @inner_content %>
  </body>
</html>
```

```html title="app.html.heex"
<main class="container">
  <%= @inner_content %>
</main>
```

```html title="live.html.heex"
<main class="container2">
  ...
  <%= @inner_content %>
</main>
```

Root layout is set it the router pipelines, default is the browser pipeline.
This plug enables live page reload as well.

```elixir
plug :put_root_layout, {HelloLayoutsWeb.LayoutView, :root}
```
