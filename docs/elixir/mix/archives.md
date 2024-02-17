# Archives

## Erlang Archives

Erlang archives are zip arhives and have`.ez` extension.

Build the current project:

```shell
mix archive.build
```

## Working with mix Archives

### Commands

List listalled archives:

```shell
mix archive
```

Archive project tasks are globally available when installed.

Example:

```shell
mix escript.install hex mix_audit
```

`mix_audit` will be listed when running `mix archive` and can be run locally for the project:

```shell
mix deps.audit .
```

Install a hex archive:

```shell
mix archive.install hex <package>
mix archive.install hex <package> <version>
```

Install a local archive:

```shell
mix archive.install archive.ez
mix archive.install path/to/archive.ez
```

Install GitHub archive

```shell
mix archive.install git https://path/to/git/repo
mix archive.install git https://path/to/git/repo branch git_branch
```

Uninstall an archive

```shell
mix archive.uninstall <package>
```

### Examples

```shell
mix archive.install hex phx_new
```

```shell
mix archive
```
```output
* hex-1.0.1
* phx_new-1.6.11
```

```shell
mix archive.uninstall phx_new
```

```shell
mix archive
```
```output
* hex-1.0.1
```

```shell
mix archive.install hex phx_new
```

## Resources

* [Loading of Code From Archive Files. Erlang Docs.](https://www.erlang.org/doc/man/code.html#loading-of-code-from-archive-files)
* [Proposed changes to the Erlang archives - are you using them? erlang forums.](https://erlangforums.com/t/proposed-changes-to-the-erlang-archives-are-you-using-them/2269)
