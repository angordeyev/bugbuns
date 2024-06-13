# String

## Transformations

Change:

```rust
let mut a = String::from("hello");
```

## Indented Multilne String

Using evcxr:

```rest
:dep indoc = { version = "2" }
use indoc::indoc;

let indented: &str = indoc! {"
  1
    2
"};

println!("{indented}");
```

```output
1
  2
```

## Resources

* [indoc crate](https://crates.io/crates/indoc)
