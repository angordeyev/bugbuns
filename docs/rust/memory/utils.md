---
draft: true
---

# Utils

## Get a Value Type

```rust
fn type_of<T>(_: T) -> &'static str {
    std::any::type_name::<T>()
}

fn main() {
    let a = 1;
    let a_ref = &a;
    println!("a: {}", type_of(a));
    println!("a ref: {}", type_of(&a));
    println!("a ref: {}", type_of(a_ref));
}
```

```rust
std::any::type_name_of_val(&1.1)
```

## Get a type Size

```rust
use std::mem;

std::mem::size_of::<i32>()
```

## Get a Value Size

```rust
use std::mem;

let a = 1;
mem::size_of_val(&a)
```

```rust
{
    use std::mem;

    let a = 1i32;
    let b = a;
    let ra = &a;

    assert_eq!(mem::size_of_val(&a), 4);
    assert_eq!(mem::size_of_val(&b), 4);
    assert_eq!(mem::size_of_val(&ra), 8);
}
```

## Get a Memory Address

```rust
{
    let a = String::from("text");
    let a_ref_1 = &a;
    let a_ref_2 = &a;

    println!("a stack addr {:p}", a_ref_1);
    println!("a stack addr {:p}", a_ref_2);
    println!("a heap  addr {:p}", a_ref_1.as_ptr());
}
```

```rust
{
    let a = String::from("text");
    let a_ref = &a;

    println!("a stack addr {:p}", a_ref);
    println!("a stack addr {:p}", &a);

    println!("---");

    println!("a heap  addr {:p}", a_ref.as_ptr());
    println!("a heap  addr {:p}", a.as_ptr());
    println!("a heap  addr {:p}", (&a).as_ptr());

    println!("---");

    println!("a heap  addr {:p}", &a.as_ptr());
    println!("a heap  addr {:p}", &a.as_ptr());
}
```

```output
a heap  addr 0x60c1cf29ad00
a heap  addr 0x60c1cf29ad00
a heap  addr 0x60c1cf29ad00
a heap  addr 0x7ffe0d30b728
```

## Get Stack Size

## Resources

* [How to get the current stack frame depth in Rust? StackOverflow.](https://stackoverflow.com/questions/69141478/how-to-get-the-current-stack-frame-depth-in-rust)
