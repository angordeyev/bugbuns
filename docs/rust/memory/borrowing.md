---
draft: true
---

# Borrowing

When a stack variable is assigned to another no borrowing occurs because it is copied. When a heap variable is assigned to another no borrowing occurs because it is moved.

Making a reference borrows a variable:

```rust
fn main() {
    let mut a = 1;

    // `a` is borrowed here
    let b = &a;

    a = 2;

    println!("b: {b}");
    // `a` is released after the last use by b

    println!("a: {a}");
}
```

```output
[E0506] Error: cannot assign to `a` because it is borrowed
   ╭─[command:1:1]
   │
 3 │     let b = &a;
   ·             ─┬
   ·              ╰── `a` is borrowed here
   ·
 5 │     a = 2;
   ·     ──┬──
   ·       ╰──── `a` is assigned to here but it was already borrowed
   ·
 7 │     println!("b: {b}");
   ·                  ─┬─
   ·                   ╰─── borrow later used here
───╯
```

Let's rewrite it without an error output:

```rust
fn main() {
    let mut a = 1;

    // `a` is borrowed here
    let b = &a;

    println!("b: {b}");
    // `a` is released after the last use by b

    a = 2;
    println!("a: {a}");
}
```

```output
b: 1
a: 2
```

Multiple references:

```rust
fn main() {
    let a = 1;

    // `a` is borrowed here
    let b = &a;
    let c = &a;

    println!("a: {a}");
    println!("b: {b}");
    println!("c: {c}");
}
```


```rust
let a = 1;

// The passed argument will be copied to the function parameter
fn some_function(x: i32) {
  println!("{x}");
}

some_function(a);

println!("{a}");

```output
1
1
```

`println!` does not borrow a varibale because it's a macro that uses a reference.

```rust
let a = String::from("text");
println!("{a}");
println!("{a}");
```

```output
text
text
```

```rust
let a = String::from("text");

// The passed argument will be copied to the function parameter
fn some_function(x: String) {
  println!("{x}");
}

some_function(a);

println!("{a}");
```

```output
[E0382] Error: borrow of moved value: `a`
    ╭─[command:1:1]
    │
  1 │ let a = String::from("text");
    ·     ┬
    ·     ╰── move occurs because `a` has type `String`, which does not implement the `Copy` trait
    ·
  8 │ some_function(a);
    ·               ┬│
    ·               ╰── value moved here
    ·                │
    ·                ╰─ help: consider cloning the value if the performance cost is acceptable: `.clone()`
    ·
 10 │ println!("{a}");
    ·           ─┬─
    ·            ╰─── value borrowed here after move
────╯
```

```rust
let a = String::from("text");
let b = some_function(a);

// Returns ownership of x with the result
fn some_function(s: String) -> String {
    s
}

println!("{}", b);
```

```output
text
```

```rust
let a = String::from("text");

fn calc_with_reference(s: &String) -> usize {
    s.len()
}

println!("{}",calc_with_reference(&a));
```

```output
4
```

## References

```rust
{
    let a = 1;
    let b = &a;

    println!("a: {a}");
    println!("b: {b}");
}
```

```output
a: 1
b: 1
```

Closures borrow variables:

```rust
fn main() {
    let mut a = 1;
    let a_closure  = || a;
    a = 2;
    println!("a: {}", a);
    println!("a_closure: {}", a_closure());
}
```

```output
error[E0506]: cannot assign to `a` because it is borrowed
 --> src/main.rs:4:5
  |
3 |     let a_closure  = || a;
  |                      -- - borrow occurs due to use in closure
  |                      |
  |                      `a` is borrowed here
4 |     a = 2;
  |     ^^^^^ `a` is assigned to here but it was already borrowed
5 |     println!("a: {}", a);
6 |     println!("a_closure: {}", a_closure());
  |                               --------- borrow later used here
```

```rust
{
    let mut a = vec!(1,2,3);
    let b = &a;
    let c = &a;
    println!("b: {:?}", b);
    println!("c: {:?}", c);
}
```

```
b: [1, 2, 3]
c: [1, 2, 3]
```


```rust
{
    let mut a = vec!(1,2,3);
    let a_closure  = || a;
    let c = &a;

    println!("a: {:?}", a);
    println!("c: {:?}", c);
    println!("a_closure: {:?}", a_closure());
}
```

```output
[E0382] Error: borrow of moved value: `a`
   ╭─[command:1:1]
   │
 2 │     let mut a = vec!(1,2,3);
   ·         ──┬──
   ·           ╰──── move occurs because `a` has type `Vec<i32>`, which does not implement the `Copy` trait
 3 │     let a_closure  = || a;
   ·                      ─┬ ┬
   ·                       ╰──── value moved into closure here
   ·                         │
   ·                         ╰── variable moved due to use in closure
 4 │     let c = &a;
   ·             ─┬
   ·              ╰── value borrowed here after move

```

