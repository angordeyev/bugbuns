---
draft: true
---

# Option

```rust
let o: Option<i32> = None;
assert_eq!(o, None);
```

## Unwrap

Successful:

```rust
let o: Option<i32> = Some(1);
assert_eq!(o, Some(1));
assert_eq!(o.unwrap(),1);
```

Error:

```rust
fn main() {
    let o: Option<i32> = None;
    let o_unwrapped = o.unwrap();
    println!("{o_unwrapped}");
}
```

```shell
cargo run; echo $?
```

```output
thread 'main' panicked at src/main.rs:3:25:
called `Option::unwrap()` on a `None` value
...
101
```

The application returns the error code 101.

## let-else, if-let, while-let

let-else:

```rust
let a = Some(1);
let Some(b) = a else {
    panic!("Can't read");
};
```

if-let:

```rust
let a = Some(1);
if let Some(b) = a {
    println!("hi");
};
```

while-let:

```rust
let mut v = vec!(1,2,3);
while let Some(i) = v.pop() {
    println!("{}", i);
}
```
