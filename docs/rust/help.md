---
draft: true
---

# Help

## Cheats

## Docs

### Web

[Rust std docs (doc.rust-lang.org/stable/std/)](https://doc.rust-lang.org/stable/std/)

Search keys are <kbd>s</kbd>> and <kbd>S</kbd>>. Autocomlete works.

### Evcxr

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

## Types

[Basic Types Cheatsheet](https://cheats.rs/#basic-types)

Get a value type:

```rust
let a = 1;
std::any::type_name_of_val(&a)
```

```output
"i32"
```

```rust
std::any::type_name_of_val(&1.1)
```

```output
"f64"
```

Get a value size:

```rust
let a = 1;
std::mem::size_of_val(&a)
```

```output
4
```

```rust
std::mem::size_of_val(&1.1)
```

```output
8
```

## Resources

 * [How to read this documentation. std crate docs.](https://doc.rust-lang.org/stable/std/index.html#how-to-read-this-documentation)
 * [Rust by Example](https://doc.rust-lang.org/rust-by-example/)
 * [rustlings](https://rustlings.cool/)
