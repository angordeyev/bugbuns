# Tasks

## Use the Previous Command Argument

```shell
mkdir <dir-name> && cd $_
```

## Shell Prompt

Posix Compatible:

```shell
printf 'Is this a good question (y/n)? '
read answer
```

```shell
printf 'Enter port number (default 8888): '
read port
if [ "${port}" = "" ] ;then
  port=8888
fi
```

## Compare Directories

Using meld:

```shell
meld directory_1 directory_2
```

Using diff:

```shell
diff -qr directory_1 directory_2
```

## Footnotes

[^substitute]: substitute - заменить
