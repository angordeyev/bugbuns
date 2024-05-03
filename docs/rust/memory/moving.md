---
draft: true
---

# Moving

Heap variables are moved.

On assigning:

```rust
{
    let a = String::from("text");
    let b = a;
    (a,b)
}
```

```output
[E0382] Error: use of moved value: `a`
   ╭─[command:1:1]
   │
 2 │     let a = String::from("text");
   ·         ┬
   ·         ╰── move occurs because `a` has type `String`, which does not implement the `Copy` trait
 3 │     let b = a;
   ·             ┬│
   ·             ╰── value moved here
   ·              │
   ·              ╰─ help: consider cloning the value if the performance cost is acceptable: `.clone()`
 4 │     (a,b)
   ·      ┬
   ·      ╰── value used here after move
───╯
```

```rust
let mut a = vec!(1,2,3);
let b = a;
a.push(4);
```

```output
[E0382] Error: borrow of moved value: `a`
   ╭─[command:1:1]
   │
 1 │ let mut a = vec!(1,2,3);
   ·     ──┬──
   ·       ╰──── move occurs because `a` has type `Vec<i32>`, which does not implement the `Copy` trait
 2 │ let b = a;
   ·         ┬│
   ·         ╰── value moved here
   ·          │
   ·          ╰─ help: consider cloning the value if the performance cost is acceptable: `.clone()`
 3 │ a.push(4);
   · ┬
   · ╰── value borrowed here after move
───╯
```

On function call:

```rust
fn print_text(text: String) {
    println!("{text}");
}

{
    let a = String::from("text");
    print_text(a);
    let b = a;
    (a,b)
}
```

```output
[E0382] Error: use of moved value: `a`
   ╭─[command:1:1]
   │
 6 │     let a = String::from("text");
   ·         ┬
   ·         ╰── move occurs because `a` has type `String`, which does not implement the `Copy` trait
 7 │     print_text(a);
   ·                ┬│
   ·                ╰── value moved here
   ·                 │
   ·                 ╰─ help: consider cloning the value if the performance cost is acceptable: `.clone()`
 8 │     let b = a;
   ·             ┬
   ·             ╰── value used here after move
```

On closure call:

```rust
{
    let a = String::from("text");
    let print_text = |text| println!("{text}");
    print_text(a);
    let b = a;
    (a,b)
}
```

```output
[E0382] Error: use of moved value: `a`
   ╭─[command:1:1]
   │
 2 │     let a = String::from("text");
   ·         ┬
   ·         ╰── move occurs because `a` has type `String`, which does not implement the `Copy` trait
   ·
 4 │     print_text(a);
   ·                ┬│
   ·                ╰── value moved here
   ·                 │
   ·                 ╰─ help: consider cloning the value if the performance cost is acceptable: `.clone()`
 5 │     let b = a;
   ·             ┬
   ·             ╰── value used here after move
───╯

```

Borrow on closure assignment:

```rust
{
    let a = String::from("text");
    let print_text = || a;
    let b = a;
    print_text();
    (a,b)
}

```output
[E0382] Error: use of moved value: `a`
   ╭─[command:1:1]
   │
 2 │     let a = String::from("text");
   ·         ┬
   ·         ╰── move occurs because `a` has type `String`, which does not implement the `Copy` trait
 3 │     let print_text = || a;
   ·                      ─┬ ┬
   ·                       ╰──── value moved into closure here
   ·                         │
   ·                         ╰── variable moved due to use in closure
 4 │     let b = a;
   ·             ┬
   ·             ╰── value used here after move

```

Reassign:

```rust
let mut a = String::from("text");

let b = a;
// Variable a is invalid because it is moved

a = String::from("new text");
// Variable is valid after reassign

println!("a: {a}");
println!("b: {b}");
```

```output
a: new text
b: text
```

Variable cannot be used after it's value is moved:

```rust
let mut a = vec!(1,2,3);
let b = a;
vec!(4,5,6).extend(a);
```

```output
[E0382] Error: use of moved value: `a`
   ╭─[command:1:1]
   │
 1 │ let mut a = vec!(1,2,3);
   ·     ──┬──
   ·       ╰──── move occurs because `a` has type `Vec<i32>`, which does not implement the `Copy` trait
 2 │ let b = a;
   ·         ┬│
   ·         ╰── value moved here
   ·          │
   ·          ╰─ help: consider cloning the value if the performance cost is acceptable: `.clone()`
 3 │ vec!(4,5,6).extend(a);
   ·                    ┬
   ·                    ╰── value used here after move
───╯
```

## Resources

* [Why am I able to re-assign to a moved variable? StackOverflow.](https://stackoverflow.com/questions/64358363/why-am-i-able-to-re-assign-to-a-moved-variable)
