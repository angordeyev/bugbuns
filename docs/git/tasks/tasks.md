# Tasks

## Getting Help

List commands:

```shell
git help
```

List all commands:

```shell
git help -a
```

Get a command help:

```shell
git help branch
git branch --help
```

## Get one File from a Branch

```shell
git restore --source <branch-name> -- <file>
```

## Delete a Branch

Delete a local branch:

```shell
git branch -d <branch-name>
```

Force delete a local branch:

```shell
git branch -D <branch-name>
```

Delete a remote branch:

```shell
git push origin -d <branch-name>
```

## Create a Names Stash

The short version:

```shell
git stash -m <stash-name>
```

The long version:

```shell
git stash push -m <stash-name>
```

## List Stashes

```shell
git stash list
```

## Apply Stash by Name

```shell
git stash apply stash^{/stash-name}
```

## List a Remote Repo Tags

```shell
git ls-remote --tags --sort="v:refname" <repo_addres>
```

## Remove Untracked Files

Without `.gitignore` files:

```shell
git clean -fd
```

With `.gitignore` files:

```shell
git clean -fdx
```
