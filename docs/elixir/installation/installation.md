# Installation

## asdf

### Prerequisites

Install asdf from [asdf-vm.com](https://asdf-vm.com)

Update `~/.bashrc` with `export KERL_BUILD_DOCS=yes` to

Install Plugins:

```shell
asdf plugin add erlang
asdf plugin add elixir
```

### Install

List available versions:

```shell
asdf list all erlang
asdf list all elixir
```

Install Elixir and Erlang:

```shell
KERL_BUILD_DOCS=yes KERL_INSTALL_MANPAGES=yes KERL_INSTALL_HTMLDOCS=yes asdf install erlang <version>
asdf install elixir <version>
```

Install Livebook

```shell
mix escript.install hex livebook
asdf reshim
```

### List All Available Versions

```shell
asdf list all erlang
asdf list all elixir
```

### Set Global Default Versions

```shell
asdf global erlang 25.1.2
asdf global elixir 1.14
```

### Show Default Global Verions

```shell
asdf current
```

### Setting asdf version of Elixir and Erlang OTP

[Elixir School - Agnostic Version Management With asdf](https://elixirschool.com/blog/asdf-version-management/)

Examples:

```shell
asdf local erlang ref:OTP-19.3-patched; asdf local elixir 1.4.5-otp-19
asdf local erlang 20.3
asdf local elixir 1.7.0-otp-20
```

### Uninstall

```shell
asdf uninstall erlang <version>
asdf uninstall elixir <version>
```

## Ubuntu 22

### Build Host

Unattanded security updates  are enable by default in Ubuntu.

To create a build and run projects:

```shell
sudo apt update && sudo apt upgrade

# install PostgreSQL
sudo apt install postgresql
sudo -u postgres psql
postgres=# \password postgres
postgres=# exit

sudo apt install erlang
sudo apt install elixir

sudo apt install inotify-tools
```

Create a new project:

```shell
mix archive.install hex phx_new
# Could not find Hex, which is needed to build dependency :phx_new
# Shall I install Hex? (if running non-interactively, use "mix local.hex --force") [Yn]

y # agree to install Hex

mix phx.new hello_phx

mix setup
# Could not find "rebar3", which is needed to build dependency :ranch
# I can install a local copy which is just used by Mix
# Shall I install rebar3? (if running non-interactively, use "mix local.rebar --force") [Yn]

y # agree to install rebar3
```

Prepare a release:

```shell
mix phx.gen.release
MIX_ENV=prod mix release

mix phx.gen.secret
export SECRET_KEY_BASE=<SECRET>
export DATABASE_URL=ecto://postgres:postgres@localhost/hello_phx

MIX_ENV=prod mix ecto.setup
```

Generate a release:

```shell
MIX_ENV=prod mix assets.deploy
MIX_ENV=prod mix release
```

Run a release:

```shell
_build/prod/rel/hello_phx/bin/server
```

Access release in a browser at `server_ip_address:4000`

### Release Host

#### Initial Setup

```shell
sudo apt update && sudo apt upgrade

sudo useradd webapp
sudo mkdir /srv/webapps
sudo chown webapp:webapp /srv/webapps

# install PostgreSQL
sudo apt install postgresql

# set postgres password
sudo -u postgres psql
postgres=# \password postgres
postgres=# \q
```

## Installing Using Nix

[What is the canonical way of installing Elixir or Erlang > 19 with `nix` on a non-NixOS system? StackOverflow.](https://stackoverflow.com/questions/51371028/what-is-the-canonical-way-of-installing-elixir-on-erlang-19-with-nix-on-a-no/51384383#51384383)
[Elixir 1.5.1 with Erlang 20.0 on NixOS 18.03? Reddit.](https://www.reddit.com/r/NixOS/comments/73ceks/elixir_151_with_erlang_200_on_nixos_1803/)
