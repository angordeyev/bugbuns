---
draft: true
---

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

Using blocks with match:

```rust
let x = 1;

match x {
  1 =>
      let a = 1;
      a+2,

  _ => x*x
}
```

```output
Error: expected expression, found `let` statement
   ╭─[command:1:1]
   │
 3 │     let a = 1,
   ·     ─┬─
   ·      ╰─── error: expected expression, found `let` statement
───╯
Error: expected one of `,`, `=>`, `@`, `if`, `|`, or `}`, found `+`
   ╭─[command:1:1]
   │
 4 │     a+2,
   ·      ┬
   ·      ╰── expected one of `,`, `=>`, `@`, `if`, `|`, or `}`
───╯
```

```rust
let x = 1;

match x {
    1 => {
        let a = 1;
        a + 2
    }

    _ => x * x
};
```

Match on a reference:

```rust
struct Point {
    x: i32,
    y: i32,
}

let p = Point{x: 1, y: 2};

match p {
    Point{x: 1, y: 2} => println!("hello"),
    _ => println!("bye"),
}

let p1 = p;
```
