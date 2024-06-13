---
draft: true
---

# Const

Shadow a variable:

```rust
const a = 1;
```

```output
Error: missing type for `const` item
```

```rust
const a = 1i32;
```

```output
Error: missing type for `const` item
```

```rust
const a: i32 = 1;
```

## Resouces

* [Why is type declaration necessary in constants? HadrienG. Rust programming language users forum.](https://users.rust-lang.org/t/why-is-type-declaration-necessary-in-constants/14200/5?u=angordeyev)
