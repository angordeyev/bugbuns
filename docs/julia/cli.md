# Julia cmd

Evaluate code

```shell
julia -e 'println("hello")'
```

Evaluate code and run interactive shell

```shell
julia -ie 'println("hello")'
```

Multiline

```shell
julia -ie '
module M
  greet() = print("hello")
end
M.greet()
'
```
