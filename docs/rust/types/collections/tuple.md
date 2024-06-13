# Tuple

## Initialize

```rust
let a: (i32, f64, String) = (1,2.2,String::from("Hello"));
std::any::type_name_of_val(&a)
```

```output
"(i32, f64, alloc::string::String)"
```

## Get an Element by Index

```rust
let t = (1, 1.2, "hello");
assert_eq!(t.1, 1.2);
```

## Named Tuple (Tuple Struct)

```rust
struct Pair(i32, i32);
let pair = Pair(1,2);
std::any::type_name_of_val(&pair)
```

```output
"ctx::Pair"
```
