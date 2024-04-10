# Rust

## Memory Locations

* Static (initialized at compile time)
* Stack  (the size is known at compile time, initialized at run time)
* Heap

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
let a = 1;
println!("1: {a}");

{
  // shadows the variable in the current block
  let a = 2;
  println!("2: {a}");
}

println!("3: {a}");

// shadows the variable
let a = 4;
println!("4: {a}");
```

```output
1: 1
2: 2
3: 1
4: 4
```

## Copying and Moving

```rust
let mut a = 1;
// the value is copied from a to b
let b = a;

a = 2;

println!("a: {a}");
println!("b: {b}");
```

```output
a: 2
b: 1
```

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

## Burrowing

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

```rust
let a = String::from("text");
println!("{}", a);
println!("{}", a);
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

## Resources

* [Chapter 5 - Ownership & Borrowing Data. Tour of Rust.](https://tourofrust.com/chapter_5_en.html)
* [Rust #14. Концепция владения, ссылки, срезы в Rust. BRO-IT.](https://www.youtube.com/watch?v=yx1dtx9fHZI)
* [Rust Memory Layout and Types. Breno Rocha, amindWalker.](https://github.com/amindWalker/Rust-Layout-and-Types)
* [Data segment. Wikipedia.](https://en.wikipedia.org/wiki/Data_segment)
