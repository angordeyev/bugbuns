# Stash

## Help

```shell
git stash --help
```

## List Stash Entries

```shell
git stash list
```

## Push Named Stash

```shell
git stash push -m <stash_name>
```

## Apply Stash by Name

```shell
git stash apply stash^{/<stash_name>}
```

## Put Seleted Files to Stash

```shell
git stash push <file1> <file2>
```
