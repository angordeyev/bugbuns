# Git

## Tasks

### Remove a File From Staging (Unstage)

```sh
git rm --staged <file_name>
```

### Unstage All Files

```sh
git reset HEAD -- .
```

### Show Staged Diffs

```sh
git diff --staged
```

### Edit the Last Commit Message

```sh
git commit --amend
```

Edit the message in a text editor and save before quit.

```sh
git push --force
```

### Change Last n Commits

```sh
git rebase -i HEAD~<n>
```

Edit the commits.

```sh
git push --force
```

### Clone the Latest Version Only

```sh
git clone --depth=1 <remote_repo_url>
```

### Rename the Current Branch

```sh
git branch -m <newname>
```

### Add Changes to the Last Commit

```sh
git add <changes>
git commit --amend --no-edit
git push --force
```

### Rebase with a Branch

```sh
git checkout develop
git checkout <feature_branch>
git rebase develop
```

### Change the Author and the Commiter for the Last n Commits

```sh
git rebase -i HEAD~1 -x "GIT_COMMITTER_NAME='a.gordeev' GIT_COMMITTER_EMAIL='<a.gordeev@fun-box.ru>' git commit --amend --author 'a.gordeev <a.gordeev@fun-box.ru>' --no-edit"
```

### Delete a Branch

Delete a local branch

```sh
git branch -d <local-branch>
```

Delete a remote branch

```sh
git push origin -d <remote-branch>
```

### Rename a Branch

Rename a local branch

```sh
git branch -m <new-name>
```

```sh
git branch -m <old-name> <new-name>
```

## Show Remote Repositories

```sh
git remote -v
```

Push the new branch and you can delete the old remote branch after renaming.

### General

```
Remove from staging (unstage)
git rm --staged <file_name>
Unstage all files
git reset HEAD -- .

Push branch and select origin, so will not need to enter origin again
git push -u origin <branch_name>

# checkout all unstaged files
git checkout . ## can be used safely,
git checkout -- . ## -- tells that following text is not a branch:
# if file "a" and branch "a" do exist, "git checkout a" will checkout branch and "git checkout -- a" will checkout file
-- as a standalone argument (i.e. not part of another argument) is used by many UNIX command.
```

## Branches

Default branch is `main` now. Set the default branch globally.

```shell
git config --global init.defaultBranch main
```

## Links

[Just a simple guide for getting started with git. no deep shit ;)](https://rogerdudler.github.io/git-guide/)

## Tips

Slow commands:
Be careful with binary files, they make status commands slow
