---
draft: true
---

# Memory Layout

Create a program:

```rust title="main.rs"
const C1: i8 = 1;
const C2: i8 = 1;
const C3: i8 = 2;
const C4: &str = "1";
const C5: &str = "1";
const C6: &str = "2";

fn main() {
    println!("C1 addr {:p}",&C1);
    println!("C2 addr {:p}",&C2);
    println!("C3 addr {:p}",&C3);
    println!("C4 addr {:p}",&C4);
    println!("C5 addr {:p}",&C5);
    println!("C6 addr {:p}",&C6);
    println!();
    let a = 1;
    let b = 2;
    println!("a addr {:p}", &a as *const i32);
    println!("b addr {:p}",&b);
    println!();
    inner();
    let d = 5;
    let e = 6;
    println!("d addr {:p}",&d);
    println!("e addr {:p}",&e);
    println!();
    let f = vec!(1,2,3);
    let f_ref = &f;
    println!("f stack addr {:p}", f_ref);
    println!("f heap  addr {:p}", f_ref.as_ptr());
}

#[inline(never)]
fn inner() {
    let c = 4;
    println!("d addr {:p}",&c);
    println!();
}
```

Compile and run:

```
rustc main.rs && \
# run main with turned of
setarch --verbose --addr-no-randomize ./main
```


```output
C1 addr 0x55555559b0a4
C2 addr 0x55555559b0a4
C3 addr 0x55555559b0a5
C4 addr 0x5555555aa258
C5 addr 0x5555555aa258
C6 addr 0x5555555aa2b0

a addr 0x7fffffffd380
b addr 0x7fffffffd384

d addr 0x7fffffffd05c

d addr 0x7fffffffd448
e addr 0x7fffffffd44c

f stack addr 0x7fffffffd510
f heap 0x5555555aeaa0
```

## Resources

* [Does stack grow upward or downward? Reddit](https://www.reddit.com/r/ProgrammerHumor/comments/r4z4no/does_stack_grow_upward_or_downward/)
* [Does stack grow upward or downward?](https://stackoverflow.com/questions/1677415/does-stack-grow-upward-or-downward)
* [Why do subsequent Rust variables increment the stack pointer? StackOverflow.](https://stackoverflow.com/questions/54395558/why-do-subsequent-rust-variables-increment-the-stack-pointer-instead-of-decremen)
* [Sparkplug — a non-optimizing JavaScript compiler](https://v8.dev/blog/sparkplug)
