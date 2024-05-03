---
draft: true
---

# Rust

## Memory Locations

* Data Memory (initialized at compile time)
* Stack Memory (the size is known at compile time, initialized at run time)
* Heap Memory

## Binding and Ownership

```rust
fn main() {
    // We instantiate value and bind to variables to create memory resources.
    // a is the owner of value 1 in memory.
    let a = 1;

    // a is dropped at the end of the scope
}
```

## Shadowing

```rust
fn main() {
    let a = 1;
    let ref_a_1 = &a;

    let a = 2;
    let ref_a_2 = &a;

    println!("ref_a_1: {}", ref_a_1);
    println!("ref_b_2: {}", ref_a_2);
}
```

```output
1: 1
2: 2
```

```rust
fn main() {
    let a = 1;
    let a_closure_1  = || a;

    let a = 2;
    let a_closure_2  = || a;

    println!("a_closure_1(): {}", a_closure_1());
    println!("a_closure_2(): {}", a_closure_2());
}
```

```output
a_closure_1(): 1
a_closure_2(): 2
```

```rust
let a = 1;
println!("1: {a}");

{
  // shadows the variable in the current block
  let a = 2;
  println!("2: {a}");
}

println!("3: {a}");

let ref_a = &a;

// shadows the variable
let a = 4;
println!("4: {a}");

println!("5: {}", *ref_a);
```

```output
1: 1
2: 2
3: 1
4: 4
5: 1
```

# Moving

Heap variables are moved:

```rust
let a = String::from("text");
// the value is moved from a to b
let b = a;

println!("{a}");
println!("{b}");
```

```output
[E0382] Error: borrow of moved value: `a`
   ╭─[command:1:1]
   │
 1 │ let a = String::from("a");
   ·     ┬
   ·     ╰── move occurs because `a` has type `String`, which does not implement the `Copy` trait
 2 │ let b = a;
   ·         ┬│
   ·         ╰── value moved here
   ·          │
   ·          ╰─ help: consider cloning the value if the performance cost is acceptable: `.clone()`
   ·
 4 │ println!("{a}");
   ·           ─┬─
   ·            ╰─── value borrowed here after move
```

`mut` modifier can be changed when moving:

```rust
let a = String::from("text");
let mut b = a;
b = String::from("new text");
println!("{b}");
```

```output
new text
```

## Mutability

Trying to reassign immutable variable:

```rust
let a = 1;
a = 2;
println!("{a}");
```

```output
[E0384] Error: cannot assign twice to immutable variable `a`
   ╭─[command:1:1]
   │
 1 │ let a = 1;
   ·     ┬
   ·     ╰── first assignment to `a`
   ·     │
   ·     ╰── help: consider making this binding mutable: `mut a`
 2 │ a = 2;
   · ──┬──
   ·   ╰──── cannot assign twice to immutable variable
   ·
   · Note: You can change an existing variable to mutable like: `let mut x = x;`
───╯
```

Reassign a mutable variable:

```rust
let mut a = 1;
a = 2;
println!("{a}");
```

```output
2
```

References:

```rust
let a = 1;
let b = 2;

let mut c = &a;

println!("c1: {c}");

c = &b;

println!("c2: {c}");
```

```output
c1: 1
c2: 2
```

Trying to reate a mutable reference to an immutable variable:

```rust
{
    let a = 1;
    let  _b = &mut a;
}
```

```outut
[E0596] Error: cannot borrow `a` as mutable, as it is not declared as mutable
   ╭─[command:1:1]
   │
 2 │     let a = 1;
   ·         │
   ·         ╰─ help: consider changing this to be mutable: `mut `
 3 │     let  _b = &mut a;
   ·               ───┬──
   ·                  ╰──── cannot borrow as mutable
   ·
   · Note: You can change an existing variable to mutable like: `let mut x = x;`
───╯
```

Create an immutable reference to an mutable variable:

```rust
{
    let mut a = 1;
    let b = &a;

    println!("b: {b}");
}
```

```output
b: 1
```

```rust
{
    let mut a = 1;
    let b = &a;

    *b += 1;
}
```

```output
[E0594] Error: cannot assign to `*b`, which is behind a `&` reference
   ╭─[command:1:1]
   │
 3 │     let b = &a;
   ·              │
   ·              ╰─ help: consider changing this to be a mutable reference: `mut `
   ·
 5 │     *b += 1;
   ·     ───┬───
   ·        ╰───── `b` is a `&` reference, so the data it refers to cannot be written
───╯
```

Create a mutable reference to a mutable variable:

```rust
{
    let mut a = 1;
    let b = &mut a;

    *b += 1;

    println!("a: {a}");
}
```

```output
a: 2
```

Borrow twice immutable:

```rust
{
    let a = 1;
    let b = &a;
    let c = &a;

    println!("{b}");
    println!("{c}");
}
```

Try to borrow twice mutable:

```rust
{
    let mut a = 1;
    let b = &mut a;
    let c = &mut a;

    println!("{b}");
    println!("{c}");
}
```

```output
[E0499] Error: cannot borrow `a` as mutable more than once at a time
   ╭─[command:1:1]
   │
 3 │     let b = &mut a;
   ·             ───┬──
   ·                ╰──── first mutable borrow occurs here
 4 │     let c = &mut a;
   ·             ───┬──
   ·                ╰──── second mutable borrow occurs here
   ·
 6 │     println!("{b}");
   ·               ─┬─
   ·                ╰─── first borrow later used here
───╯
```

Try to borrow twice: immutable then mutable:

```rust
{
    let mut a = 1;
    let b = &a;
    let c = &mut a;

    println!("{b}");
    println!("{c}");
}

```output
[E0502] Error: cannot borrow `a` as mutable because it is also borrowed as immutable
   ╭─[command:1:1]
   │
 3 │     let b = &a;
   ·             ─┬
   ·              ╰── immutable borrow occurs here
 4 │     let c = &mut a;
   ·             ───┬──
   ·                ╰──── mutable borrow occurs here
   ·
 6 │     println!("{b}");
   ·               ─┬─
   ·                ╰─── immutable borrow later used here
───╯
```

Borrow and release, borrow and relase, borrow and relase:

```rust
{
    let mut a = 1;
    println!("a: {a}");

    // borrow
    let b = &a;
    println!("b: {b}");
    // release

    // borrow
    let c = &mut a;
    println!("c: {c}");
    // release

    // borrrow
    let d = &mut a;
    println!("d: {d}");
    // release
}
```

```output
a: 1
b: 1
c: 1
d: 1
```

## Function Parameters Mutability

### A Stack Value

Immutable parameter:

```rust
let a = 1;

fn change_num(n: i32) -> i32 {
    n = n + 1;
    n
}

change_num(a);
```

```output
[E0384] Error: cannot assign to immutable argument `n`
   ╭─[command:1:1]
   │
 3 │ fn change_num(n: i32) -> i32 {
   ·               ┬
   ·               ╰── help: consider making this binding mutable: `mut n`
 4 │     n = n + 1;
   ·     ────┬────
   ·         ╰────── cannot assign to immutable argument
   ·
   · Note: You can change an existing variable to mutable like: `let mut x = x;
```

```rust
let a = 1;

// a will not change because value is copied
fn change_num(mut n: i32) -> i32 {
    n = n + 1;
    n
}

let b = change_num(a);

println!("a: {a}");
println!("b: {b}");
```

```output
a: 1
b: 2
```

### Reference to a Stack Value

```rust
{
    let a = 1;
    a
}
```

```output
1
```

```rust
{
    let a = 1;
    let b = &a;

    a
}
```

```output
1
```

```rust
{
    use std::time::Duration;
    use std::thread::sleep;

    let mut a = 1;
    let b = &a;

    a = 2;

    println!("a: {a}");
    println!("b: {b}");

    sleep(Duration::from_millis(100));
}
```

```output
1
```

```output
1
```

```rust
{
    let a = 1;
    let b = &a;

    println!("{b}");
}
```

```output
1
```

### Heap Values

```rust
let a = String::from("text");

fn change_text(s: String) {
    s.push_str(" new");
}

change_text(a);
```

```output
[E0596] Error: cannot borrow `s` as mutable, as it is not declared as mutable
   ╭─[command:1:1]
   │
 3 │ fn change_text(s: String) {
   ·                │
   ·                ╰─ help: consider changing this to be mutable: `mut `
 4 │     s.push_str("new");
   ·     ┬
   ·     ╰── cannot borrow as mutable
   ·
   · Note: You can change an existing variable to mutable like: `let mut x = x;`
```

The value is moved with 'mut' parameter:


```rust
let a = String::from("text");

fn change_text(mut s: String) {
    s.push_str(" new");
}

change_text(a);

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
 7 │ change_text(a);
   ·             ┬│
   ·             ╰── value moved here
   ·              │
   ·              ╰─ help: consider cloning the value if the performance cost is acceptable: `.clone()`
   ·
 9 │ println!("{a}");
   ·           ─┬─
   ·            ╰─── value borrowed here after move
───╯
```

```rust
fn change(x: &mut i32) {
}

fn change(mut x: &i32) {
}
```

## References

```rust
{
    let a = String::from("text");
    let b = &a;

    println!("{}", a.len());
    println!("{}", b.len());
}
```

```output
4
4
()
```

## Resources

* [Can someone explain references? r/rust Reddit.](https://www.reddit.com/r/rust/comments/v8cckf/can_someone_explain_references/)
* [Chapter 5 - Ownership & Borrowing Data. Tour of Rust.](https://tourofrust.com/chapter_5_en.html)
* [Rust #14. Концепция владения, ссылки, срезы в Rust. BRO-IT.](https://www.youtube.com/watch?v=yx1dtx9fHZI)
* [Rust Memory Layout and Types. Breno Rocha, amindWalker.](https://github.com/amindWalker/Rust-Layout-and-Types)
* [Data segment. Wikipedia.](https://en.wikipedia.org/wiki/Data_segment)
