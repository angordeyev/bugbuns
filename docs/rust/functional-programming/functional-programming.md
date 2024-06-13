# Functional Programming

Using `evcxr`:

```rust
let iter = [0,2,3,4,5].iter();
let into_iter = [0,2,3,4,5].into_iter();
```

```rust
std::any::type_name_of_val(&iter)
```

```output
core::slice::iter::Iter<i32>
```

```rust
std::any::type_name_of_val(&into_iter)
```

```output
"core::array::iter::IntoIter<i32, 5>"
```
