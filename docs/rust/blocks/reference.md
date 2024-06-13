# Reference

Reference is for borrowing.

```rust
{
    let a: i32 = 1;
    let b: &i32 = &a;
}
```

```rust
{
    let a: Vec<i32> = vec!(1,2,3);
    let b = &a;
    let c = a;
    println!("{}", b[0]);
    c[1]
}
```

```output
[E0505] Error: cannot move out of `a` because it is borrowed
   ╭─[command:1:1]
   │
 2 │     let a: Vec<i32> = vec!(1,2,3);
   ·         ┬
   ·         ╰── binding `a` declared here
 3 │     let b = &a;
   ·             ─┬
   ·              ╰── borrow of `a` occurs here
 4 │     let c = a;
   ·             ┬
   ·             ╰── move out of `a` occurs here
 5 │     println!("{}", b[0]);
   ·                    ┬
   ·                    ╰── borrow later used here
───╯
```

## Operations

```rust
use std::any::type_name_of_val;

let a = &1;
let b = 2;
let c: i32 = a + b;

println!("a type: {}, value {}", type_name_of_val(&a), a);
println!("b type: {}, value {}", type_name_of_val(&b), b);
println!("a + b type: {}, value {}", type_name_of_val(&(a + b)), (a + b));
println!("c type: {}, value {}", type_name_of_val(&c), c);
```

```output
a type: &i32, value 1
b type: i32, value 2
a + b type: i32, value 3
c type: i32, value 3
```

```rust
let a: &i32 = &1;
println!("a type: {}, value {}", type_name_of_val(&a), a);
println!("is_positive: {}", a.is_positive());
```

```rust
{
    let mut a = &1;
    let b = &mut a;
    *b = &3;
    println!("a: {a}");
}
```

```output
a: 3
```

## Dereference

```rust
let a = &1;
let b = *a;
let c = *&1;

println!("a type: {}, value {}", type_name_of_val(&a), a);
println!("b type: {}, value {}", type_name_of_val(&b), b);
println!("c type: {}, value {}", type_name_of_val(&c), c);
```

```output
a type: &i32, value 1
b type: i32, value 1
c type: i32, value 1
```

## Mutability

Immutable:

```rust
{
    let a = 1;
    let type_a = std::any::type_name_of_val(&a);
    println!("a has value {a} and type: {type_a}");

    let b: &i32 = &a;
    let type_b = std::any::type_name_of_val(&b);
    println!("b has value {b} and type: {type_b}");

    let c = &1;
    let type_c = std::any::type_name_of_val(&c);
    println!("c has value {c} and type: {type_c}");
}
```

Mutable:

```rust
{
    let a = 1;
    let b: &mut i32 = &mut a;
}
```
