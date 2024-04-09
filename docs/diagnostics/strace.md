# strace

Use grep (strace writes to stderr):

```shell
strace echo "hello" 2>&1 | grep "hello"
```
