---
draft: true
---

# Copying

Stack variables are copied:

```rust
let mut a = 1;
// the value is copied from a to b
let b = a;

a = 2;

assert_eq!(b, 1);
assert_eq!(a, 2);
```

Heap variables are moved:

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

A variable can be reassigned after move:

```rust
let mut a = vec!(1,2,3);
let b = a;
a = vec!(1,2,3,4);
```

A heap variable can be copied using clone:

```rust
let mut a = vec!(1,2,3);
let b = a;

a.push(4);

assert_eq!(a, vec!(1,2,3,4));
assert_eq!(b, vec!(1,2,3));
```

A heap variable can be copied using clone:

```rust
let mut a = String::from("text");
// the value is copied using clone
let b = a;

a = String::from("new text");

println!("a: {a}");
println!("b: {b}");
```


```rust
let mut a = String::from("text");
// the value is copied using clone
let b = a.clone();

a = String::from("new text");

println!("a: {a}");
println!("b: {b}");
```

```output
a: new text
b: text
```
