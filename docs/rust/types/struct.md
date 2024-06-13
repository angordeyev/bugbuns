---
draft: true
---

# Struct

With named fields, notice there is no semicolon at the end of the definition:

```rust
struct Point {
    x: f64,
    y: f64
}
```

With named fields, notice there is the semicolon at the end of the definition:


```rust
struct Pair(i32, i32);
```

To print add the attribute `#[derive(Debug)]`:

```rust
#[derive(Debug)]
struct Point {
    x: f64,
    y: f64
}

let p = Point{x: 1.1, y: 2.2};
p
```

```rust
#[derive(Debug)]
struct Pair(i32, i32);

let p = Pair(1,2);
p
```

## Impl

```rust
struct Pair(i32, i32);

impl Pair {
    fn sum(&self) -> i32 {
        self.0 + self.1
    }
}

let p = Pair(1,2);
p.sum()
```

```output
3
```

## Resource

* [Keyword impl](https://doc.rust-lang.org/std/keyword.impl.html)
