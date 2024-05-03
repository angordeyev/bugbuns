---
draft: true
---

# mut

`mut` modifer can be changed when copying:

```rust
let a = 1;
let b = a;
println!("a: {a}");
println!("b: {b}");
```

```output
a: 1
b: 1
```

```rust
let a = 1;
println!("a: {a}");
let mut b = 2;
println!("b: {b}");
b = 3;
println!("b: {b}");
```

```output
a: 1
b: 2
b: 3
```

```rust
let mut a = 1;
println!("a: {a}");
let b = a;
a = 2;
println!("a: {a}");
println!("b: {b}");
```

```output
a: 1
a: 2
b: 1
```
