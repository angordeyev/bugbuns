# Documentation

## General Idea

Sublimetext is for text editing, some of the features are suitable for documentation reading as well, e.g. navigation features (Goto Anything), view setup (fonts, panel sizes, etc.).

## Features

* Fast Keyboard Navigation ([Workflowy](https://workflowy.com/))
* Versions support, examples: [Docusaurus](https://docusaurus.io/), [hexdocs](https://hexdocs.pm/))
* Multilanguage support, examples: [Docusaurus](https://docusaurus.io/)
* Edit a page on GitHub, examples: [Fly.io](https://fly.io/docs/)
* Code tabs, example: [Docusaurus](https://docusaurus.io/)
* Tags, example: [Docusaurus Blogs](https://docusaurus.io/blog)
* Comments, Likes
* Files/Folders - URL mappping systems (TODO research)
* Integrations
  * Telegram. A message is converted to a document. Telegram channel and message attributes defines where the message is saved and it's properties.
* Related, example [Digital Ocean Tutorials](https://www.digitalocean.com/community/tutorials/)

#### Layout

* Full height content like [hexdocs](https://hexdocs.pm/) or menu is not fixed on top like [Sphinx](https://www.sphinx-doc.org/) 
* A current page navigation like on [Fly.io](https://fly.io/docs/) on the right side
* Breadcrumbs like in [Docusaurus](https://docusaurus.io/)

#### Panels

* Navigation
* Content
* Current Document Navigation ([Fly.io Docs](https://fly.io/docs/))
* Breadcrumbs ([Docusaurus](https://docusaurus.io/))
* Minimap (Sublimetext)
* Goto Everything (Sublimetext)
* Keyboard Shortcuts ([Workflowy](https://workflowy.com/)
* Actions (Edit in GitHub, Comment, etc.)
* Comments

#### Content Panel

* Expand/Collapse ([Workflowy](https://workflowy.com/)
* Code Tabs ([Docusaurus](https://docusaurus.io/))
* Warning ([Docusaurus](https://docusaurus.io/))

#### Navigation Panel

* Deep into link, like go into a folder in a file manger, only child links are shown after the click, the parent link may be sown at the top or not, examples: [Fly.io](https://fly.io/docs/), go to https://fly.io/docs/getting-started/ and select "Getting Started" > "Install flyctl".
* Expand/Collapse, Goto, Dive.
  * Expand/Collapse: ex
  * Goto
  * Dive hides the upper level from the left bar and shows only the lefels bellow, examples:Workflowy](https://workflowy.com/), [hex.pm](hex.pm), 
* Show/hide on a button ([Docusaurus](https://docusaurus.io/))
* Hide automatically ([Fly.io](https://fly.io/docs/))
* Tabs on the left panel, example: [hex.pm](hex.pm), "GUIDES", "MODULES", "MIX TASKS"
* Navigate to headers using scroll like [hex.pm](hex.pm)

#### Multiple Panels

* Construct panels, choose number of panels, interaction, Show/Hide Panels like in SublimeText 
* Sync the navigation panel when link is clicked in a document
* Multiple panels and sync between them
  * The left panel is navigaio, the right panel is content
  * The left panel is navigation, the middle panel is content, the right panel is code, example: [Slate](slatedocs.github.io/slate/) 

### Terminal

* Notation for terminal input and output like in [Fly.io](https://fly.io/docs/)

### Search

* [Algolia](https://www.algolia.com/)
* [typesense](https://typesense.org/)
* [Meilisearch](meilisearch.com/)
* [Elasticsearch](https://www.elastic.co/)

### Themes

* Day and night themes

## Comparations

[What are the best hosted services to render and publish markdown files online?](https://www.slant.co/topics/3845/~hosted-services-to-render-and-publish-markdown-files-online)

## Implementations

### [GitBook](https://www.gitbook.com/)

* [NATS Docs](https://nats.io/)
* [Cheat Sheets](https://jairanjankumar.gitbook.io/cheatsheet/chapter1)

### [Astro]

* [Asto Docs][https://docs.astro.build]
* [Startlight Docs](https://starlight.astro.build)

### [Docusaurus](https://docusaurus.io/)

* [RethinkDNS Docs](https://docs.rethinkdns.com/)
* [Mike Polinowski](https://mpolinowski.github.io/)

### [MiddleMan](https://middlemanapp.com/)

* [Fly.io Docs](https://fly.io/docs/])

### [VitePress](https://vitepress.dev/)

* [Mermaid](https://mermaid.js.org/intro/)

### [VuePress](https://vuepress.vuejs.org/)

* [Sublime Text Community Documentation](https://docs.sublimetext.io/)

### [MkDocs](https://www.mkdocs.org/)

* [LSP for Sublime Text](https://lsp.sublimetext.io/)

### Jekyll

* [GitHub Pages](https://pages.github.com/)
* [VictoriaMetrics Docs](https://docs.victoriametrics.com/)
* [Slate Template](https://github.com/slatedocs/slate)

## Elixir

* [Fermo](https://hexdocs.pm/fermo/middlemantofermo.html)
* [nimble_publisher](https://hex.pm/packages/nimble_publisher)

### Sites

#### [Fly.io](https://fly.io/docs/)

#### [GOV.UK developer docs](https://docs.publishing.service.gov.uk)

https://learn-to-code.london.cloudapps.digital/

**Geting started**

```shell
git clone https://github.com/alphagov/learn-to-code.git
bundle exec middleman server
```

**Repositories**

* [alphagov/learn-to-code](https://github.com/alphagov/learn-to-code)
* [alphagov/tech-docs-gem](https://github.com/alphagov/tech-docs-gem/blob/main/README.md)

## Resources

* [Jamstack](https://jamstack.org/)
* [A comments system powered by GitHub Discussions.](https://giscus.app/)
* [Middleman vs Jekyll](https://github.com/geraldb/talks/blob/master/jekyll_vs_middleman.md)
* [Docusaurus Site Showcase](https://docusaurus.io/showcase)
