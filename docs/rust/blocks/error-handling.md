# Error Handling

Create a project:

```shell
cargo new hello && cd $_
```

```shell
cargo run; echo $?
```

```output
Hello, world!
0
```

The application returns the success code 0.

## Panic

Unrecoverable:

```rust
fn main() {
    panic!("oops!");
}
```

```shell
cargo run; echo $?
```

```output
thread 'main' panicked at src/main.rs:2:5:
oops!
...
101
```

The application returns the error code 101.

## `?` operator

`?` can be is used in a function returning Result or Option.

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
    let _ = get_result();
}

fn get_result() -> Result<i32, String> {
    let r: Result<i32, String> = Err("oops!".to_string());
    println!("{}", r?);
    // returns Err Result

    println!("after");
    Ok(2)
}
```

```output
```

```rust
fn main() {
    let _ = get_result();
}

fn get_result() -> Option<i32> {
    let o: Option<i32> = Some(1);
    println!("{}", o?);
    // prints o inner value and continues

    println!("after");
    Some(2)
}
```

```output
1
after
```

```rust
fn main() {
    let _ = get_result();
}

fn get_result() -> Option<i32> {
    let o: Option<i32> = None;
    println!("{}", o?);
    // returns None Result

    println!("after");
    Some(2)
}
```
