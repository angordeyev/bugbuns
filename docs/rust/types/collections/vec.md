---
draft: true
---

```rust
vec![1,2,3]
```

```rust
let mut v = vec![1,2];
assert_eq!(v.capacity(), 2);
v.push(3);
assert_eq!(v.capacity(), 4);
v.push(4);
v.push(5);
assert_eq!(v.capacity(), 8);
```

```rust
let mut v = vec![1,2,3];
v.extend_from_slice(&[4,5,6,7,8,9]);
assert_eq!(v.capacity(), 9);
```

Print a vector:

```
println!("{:?}", vec!(1,2,3));
```

```output
[1, 2, 3]
```

## Iteration

```rust
use std::any::type_name_of_val;

let v = vec!(1,2,3);

for i in v {
    println!("i val: {} type: {}", i, type_name_of_val(&i));
}
```

```output
i val: 1 type: i32
i val: 2 type: i32
i val: 3 type: i32
```

```rust
use std::any::type_name_of_val;

let v = vec!(1,2,3);

for i in v.iter() {
    println!("i val: {} type: {}", i, type_name_of_val(&i));
}
```

```output
i val: 1 type: &i32
i val: 2 type: &i32
i val: 3 type: &i32
```

## Push

```rust
let mut v = vec!(1,2,3);
v.push(4);
println!("{:?}", v);
```

```output
[1, 2, 3, 4]
```

## Pop

```rust
let mut v = vec!(1,2,3);
if let Some(i) = v.pop() {
    println!("{i}");
};
```

```output
3
```

## Update

```rust
use std::any::type_name_of_val;

let mut v = vec!(1,2,3);

for i in v.iter_mut() {
    *i = *i*2;
}

for i in v {
    println!("i: {i}");
}
```

```output
2
4
6
```

## Resources

* [Vec. std Rust crate docs.](https://doc.rust-lang.org/std/vec/struct.Vec.html#)
