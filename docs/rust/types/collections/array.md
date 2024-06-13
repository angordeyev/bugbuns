# Array

## Initialization

With values:

```rust
let a = [1,2,3];
```

With expression `[expr; N]`:

```rust
let a = [0; 10];
```

## Type and Size

```rust
std::any::type_name_of_val(&[1,2,3])
```

```output
"[i32; 3]"
```

```rust
std::mem::size_of_val(&[1])
```

```output
4
```

```rust
std::mem::size_of_val(&[1,2,3])
```

```output
12
```
