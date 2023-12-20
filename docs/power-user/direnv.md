# direnv

## Default Configuration

Run the script:

```shell
mkdir -p ~/.config/direnv && cat << EOF > ~/.config/direnv/config.toml
[global]
load_dotenv = true
disable_stdin = true
EOF
```

Add to `.zshrc`:

```shell
export DIRENV_LOG_FORMAT= # silent
eval "$(direnv hook zsh)"
```

## Allow `direnv` in the Current Directory

```shell
direnv allow .
```

## Configure to Read `.env` Files

Create the configuration file:

```shell
mkdir -p ~/.config/direnv/ && touch $_/config.toml
```

Add to the configuration:

```toml title="~/.config/direnv/config.toml"
[global]
load_dotenv = true
```

## Resoureces

* [direnv repo](https://github.com/direnv/)
* [direnv toml](https://github.com/direnv/direnv/blob/master/man/direnv.toml.1.md)
