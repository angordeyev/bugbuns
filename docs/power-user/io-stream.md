# IO Streams

Each proces has its own IO streams:

```shell
ls -l /dev/stdin
ls -l /dev/stdout
ls -l /dev/stderr
```

```output
lrwxrwxrwx 1 root root 15 May 31 07:55 /dev/stdin -> /proc/self/fd/0
lrwxrwxrwx 1 root root 15 May 31 07:55 /dev/stdout -> /proc/self/fd/1
lrwxrwxrwx 1 root root 15 May 31 07:55 /dev/stderr -> /proc/self/fd/2
```

Write to stderr:

```shell
echo foo >> /dev/stderr
```

Experiments:

```shell
echo foo 1> /dev/stdout 2> /dev/null
```

```output
foo
```

```shell
echo foo 1> /dev/null 2> /dev/stdout
```

```output
```

```shell
echo foo 1> /dev/null 2> /dev/stdout
```

```output
```

```shell
echo foo 1> /dev/null 1> /dev/stdout
```

```
```

```shell
echo foo 1> /dev/stdout 1> /dev/null
```

```output
foo
```

```shell
echo foo 1> /dev/stdout 1> /dev/stdout
```

```output
foo
foo
```

```shell
echo foo >> /dev/null | cat
```

```output
foo
```

```shell
echo foo >> /dev/null | cat >> /dev/null
```

```output
```

```shell

```
