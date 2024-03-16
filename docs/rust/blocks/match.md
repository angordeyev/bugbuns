# Match

```shell
match "pattern" {
  "pattern" => "matched",
  _ => "not matched"
}
```

```shell
let x = 1;
let matched =
    match x {
      1 => x,
        _ => x*x
    };
println!("{matched}");
```

```rust
fn with_match(x: i32) -> i32 {
    let result =
        match x {
          1 => x,
          _ => x*x
        };
    result
}
```

