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

## Restrictions

Only mutable variable can be borrowed as mutable:

```rust
{
    let a = 1;
    let b = &mut a;
    b
}
```

```output
[E0596] Error: cannot borrow `a` as mutable, as it is not declared as mutable
   ╭─[command:1:1]
   │
 2 │     let a = 1;
   ·         │
   ·         ╰─ help: consider changing this to be mutable: `mut `
 3 │     let b = &mut a;
   ·             ───┬──
   ·                ╰──── cannot borrow as mutable
   ·
   · Note: You can change an existing variable to mutable like: `let mut x = x;`
```

```rust
{
    let mut a = 1;
    let b = &mut a;
    println!("{b}");
}
```

```output
1
```

Changing a borrowed variable:

```rust
{
    let mut a = 1;
    let mut b = &mut a;
    *b = 3;
    println!("{a}");
}
```

```output
3
```

A variable can be borrowed as mutable only once:

```rust
{
    let mut a = 1;
    let mut b = &mut a;
    let mut c = &mut a;

    println!("{b}");
    println!("{c}");
}
```

```output
[E0499] Error: cannot borrow `a` as mutable more than once at a time
   ╭─[command:1:1]
   │
 3 │     let mut b = &mut a;
   ·                 ───┬──
   ·                    ╰──── first mutable borrow occurs here
 4 │     let mut c = &mut a;
   ·                 ───┬──
   ·                    ╰──── second mutable borrow occurs here
   ·
 6 │     println!("{b}");
   ·               ─┬─
   ·                ╰─── first borrow later used here
───╯
```

Cannot assign to a borrowed variable:

```rust
{
    let mut a = 1;
    let b = &a;
    a = 2;
    (a,b)
}
```

```output
[E0506] Error: cannot assign to `a` because it is borrowed
   ╭─[command:1:1]
   │
 3 │     let b = &a;
   ·             ─┬
   ·              ╰── `a` is borrowed here
 4 │     a = 2;
   ·     ──┬──
   ·       ╰──── `a` is assigned to here but it was already borrowed
 5 │     (a,b)
   ·        ┬
   ·        ╰── borrow later used here

```

```rust
{
    let mut a = 1;
    let b = &a;
    // b releases a here because b is no longer used in the scope

    a = 2;
    a
}
```

```output
2
```

Cannot move a borrowed variable:

```rust
{
    let a = vec!(1,2,3);
    let b = &a;
    // cannot move out of `a` because it is borrowed
    let c = a;

    println!("{:?}", b);
    println!("{:?}", c);
}
```

```output
E0505] Error: cannot move out of `a` because it is borrowed
   ╭─[command:1:1]
   │
 2 │     let a = vec!(1,2,3);
   ·         ┬
   ·         ╰── binding `a` declared here
 3 │     let b = &a;
   ·             ─┬
   ·              ╰── borrow of `a` occurs here
 4 │     let c = a;
   ·             ┬
   ·             ╰── move out of `a` occurs here
 5 │     println!("{:?}", b);
   ·                      ┬
   ·                      ╰── borrow later used here
```

A borrowed variable can be copied:

```rust
{
    let a = 123;
    let b = &a;
    // cannot move out of `a` because it is borrowed
    let c = a;

    println!("{}", b);
    println!("{}", c);
}
```

```output
123
123
```

Move dereferenced:

```rust
{
    let a = vec!(1,2,3);
    // a is borrowed
    let b = &a;
    // trying to move a to c
    let c = *b;
    (a,c)
}
```

```output
[E0507] Error: cannot move out of `*b` which is behind a shared reference
   ╭─[command:1:1]
   │
 5 │     let c = *b;
   ·             ┬┬
   ·             ╰─── help: consider removing the dereference here: ``
   ·              │
   ·              ╰── move occurs because `*b` has type `Vec<i32>`, which does not implement the `Copy` trait
```

From borrowed to owned:

```rust
{
    use std::any::type_name_of_val;

    let a = vec!(1,2,3);
    // a is borrowed
    let b = &a;
    // Creates owned data from borrowed data, usually by cloning
    let c = b.to_owned();

    println!("b type: {}", type_name_of_val(&b));
    println!("c type: {}", type_name_of_val(&c));
}
```

```output
b type: &alloc::vec::Vec<i32>
c type: alloc::vec::Vec<i32>`
```

