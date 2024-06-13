---
draft: true
---

# evcxr

EVCXR - **EV**aluation **C**onte**X**t for **R**ust.

## Install

Install evcxr_repl:

```shell
cargo install --locked evcxr_repl
```

```shell
cargo install --force --git https://github.com/evcxr/evcxr.git evcxr_repl
```

## REPL

Run:

```shell
evcxr
```

Get help:

```rust
:help
```

Load a crate:

```rust
:dep indoc = { version = "2" }
```

Get a type:

```rust
let a = &1;
```

```rust
:t a
```

```output
a: &i32
```

Get doc:

```rust
:doc i32
```

```output
i32
...
The 32-bit signed integer type.
```

```rust
:doc &str::parse
```

```output
core::str
...
Parses this string slice into another type.
...
```

## Resources

* [evcxr repo](https://github.com/evcxr/evcxr)
