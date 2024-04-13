---
draft: true
---

# Types

```rust
use std::any;
```

```rust
let a = 1;
type_name_of_val(&a)
```

```output
"i32"
```

```rust
let a = 1;
let a_ref_1 = &a;
let a_ref_2 = &a;

```


```rust
{
  let a = 1;
  let a_ref = &a;
  println!("{a_ref}");
}
```

```rust
{
  let a = 1;
  println!("{a}");
}
```

```output
"&i32"
```
