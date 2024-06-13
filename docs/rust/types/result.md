---
draft: true
---

# Result

```rust
let a: Result<i32, String> = Ok(1);
assert_eq!(a, Ok(1));
assert_eq!(a?, 1);
```

## Unwrap

### `unwrap function`

```rust
fn main() {
    let r: Result<i32, String> = Ok(1);
    println!("{}", r.unwrap());
}
```

```output
1
```

### `?`operator

```rust
fn main() {
    let _ = get_result();
}

fn get_result() -> Result<i32, String> {
    let r: Result<i32, String> = Ok(1);
    println!("{}", r?);
    // prints r inner value and continues

    println!("after");
    Ok(2)
}
```

```output
1
after
```

```rust
fn main() {
    match get_result() {
        Ok(x) => println!("{x}"),
        Err(e) => println!("{e}")
    }
}

fn get_result() -> Result<i32, String> {
    let r: Result<i32, String> = Err("oops!".to_string());
    println!("{}", r?);
    // returns Err here

    println!("after");
    Ok(2)
}
```

```output
oops!
```

## Result to Option

```rust
let r1: Result<i32, String> = Err("oops!".to_string());
let r2: Result<i32, String> = Ok(1);
println!("r1: {:?}", r1);
println!("r2: {:?}", r2);
println!("r1.ok(): {:?}", r1.ok());
println!("r2.ok(): {:?}", r2.ok());
```

```output
r1: Err("oops!")
r2: Ok(1)
r1.ok(): None
r2.ok(): Some(1)
```

## Result in `main` function

```rust
fn main() -> Result<(), &'static str> {
    Ok(())
}
```

```rust
fn main() -> Result<(), &'static str> {
    Err("error")
}
```

```shell
cargo run; echo $?
```

```output
Error: "error"
1
```

## Resources

* [Result. std Rust crate docs.](https://doc.rust-lang.org/std/result/)
