# Modules

Lest's define the module:

```julia
module M
    export f

    function f()
        print("hello")
    end

    function g()
        print("hello")
    end
end
```

## `import`

```julia
julia> import M
```

With the module name

```julia
julia> M.f()
```
```output
f
```

```julia
julia> M.g()
```
```output
g
```

Without the module name

```julia
julia> f()
```
```output
ERROR: UndefVarError: `f` not defined
Stacktrace:
 [1] top-level scope
   @ REPL[4]:1
```

```julia
julia> g()
```
```output
ERROR: UndefVarError: `g` not defined
Stacktrace:
 [1] top-level scope
   @ REPL[5]:1
```

## `using`

```julia
using M
```
With the module name

```julia
julia> M.f()
```
```output
f
```

```julia
julia> M.g()
```
```output
g
```

Without the module name

```julia
julia> f()
```
```output
f
```

```julia
julia> g()
```
```output
ERROR: UndefVarError: `g` not defined
Stacktrace:
 [1] top-level scope
   @ REPL[5]:1

```




