# Terms

## HEAD

**HEAD** is a reference to the last commit in the currently check-out branch.

Lets's see an example.

Create a repository and test data:

```shell
mkdir example &&
cd example &&
git init &&

touch main &&
git add main &&
git commit -m "main"

git checkout -b a main &&
touch a1 &&
git add a1 &&
git commit -m "a1" &&

git checkout -b b a &&
touch b1 &&
git add b1 &&
git commit -m "b1" &&

git checkout -b c main &&
touch c1 &&
git add c1 &&
git commit -m "c1" &&

touch c2 &&
git add c2 &&
git commit -m "c2"

git checkout main
```

Show the repo structure:

```shell
git log --all --decorate --oneline --graph
```

```output
* 8553efa (b) b1
* 8c81a02 (a) a1
| * 8f0fc4b (c) c2
| * c93b6fb c1
|/
* cb713a2 (HEAD -> main) main
```

Draw graph using [git-sim](https://github.com/initialcommit-com/git-sim):

```shell
git sim log --all
```

You can chouse a head with the `git checkout` command:

```shell
git checkout a
git log --all --decorate --oneline --graph
```

```output
* 8553efa (b) b1
* 8c81a02 (HEAD -> a) a1
| * 8f0fc4b (c) c2
| * c93b6fb c1
|/
* cb713a2 (main) main
```

```shell
git checkout b
git log --all --decorate --oneline --graph
```

```output
* 8553efa (HEAD -> b) b1
* 8c81a02 (a) a1
| * 8f0fc4b (c) c2
| * c93b6fb c1
|/
* cb713a2 (main) main
```

```shell
git checkout c93b6fb
git log --all --decorate --oneline --graph
```

```output
* 8553efa (b) b1
* 8c81a02 (a) a1
| * 8f0fc4b (c) c2
| * c93b6fb (HEAD) c1
|/
* cb713a2 (main) main
```

Show the current HEAD:

```shell
git checkout a
git show
```

```output
commit 8c81a024f7c90f0beb05eefb99449ced8a900c86 (HEAD -> a)
...
```

## origin

**origin** is the default alias for a remote repository.

## staged, cached, index

They are synonyms.
