# Generics

A simple generic type:

```rust
struct Point<T> {
    x: T,
    y: T,
}

let p = Point {x: 1.1, y: 2.2};
println!("x: {}, y: {}", p.x, p.y);
```

