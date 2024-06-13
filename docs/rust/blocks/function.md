# Function

Simple function:

```rust
fn f() {

}
```

Function with an immutable parameter:

```rust
fn main() {
    f(1);
}

fn f(p: i32) {
    println!("{p}");
}
```

```output
1
```

```rust
fn f(p: i32) {
    println!("{p}");
    p = 3;
    println!("{p}");
}
```

```output
[E0384] Error: cannot assign to immutable argument `p`
   ╭─[command:1:1]
   │
 1 │ fn f(p: i32) {
   ·      ┬
   ·      ╰── help: consider making this binding mutable: `mut p`
   ·
 3 │     p = 3;
   ·     ──┬──
   ·       ╰──── cannot assign to immutable argument
   ·
   · Note: You can change an existing variable to mutable like: `let mut x = x;`
───╯
```

Function with a mutable parameter:

```rust
fn main() {
    let a = 1;
    println!("a1: {a}");
    f(a);
    println!("a2: {a}");
}

// i32 will be copied but copied variable can be changed
fn f(mut p: i32) {
    println!("p1: {p}");
    p = 2;
    println!("p2: {p}");
}
```

```output
a: 1
p: 1
p: 2
a: 1
```

```rust
fn main() {
    let a = vec!(1);
    println!("{:?}", a);
    println!("a stack addr {:p}", &a);
    println!("a heap  addr {:p}", (&a).as_ptr());
    // value is moved to f
    let r = f(a);
    println!("{:?}", r);
    println!("r stack addr {:p}", &r);
    println!("r heap  addr {:p}", (&r).as_ptr());
}

fn f(mut a: Vec<i32>) -> Vec<i32> {
    a.push(4);
    a
}
```
