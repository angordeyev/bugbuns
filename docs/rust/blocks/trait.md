---
draft: true
---

# Trait

```rust
struct Sheep {}
struct Cow {}

trait Animal {
    // Instance method signature
    fn noise(&self) -> &'static str;
}

// Implement the `Animal` trait for `Sheep`.
impl Animal for Sheep {
    fn noise(&self) -> &'static str {
        "baaaaah!"
    }
}

// Implement the `Animal` trait for `Cow`.
impl Animal for Cow {
    fn noise(&self) -> &'static str {
        "moooooo!"
    }
}

// Returns some struct that implements Animal, but we don't know which one at compile time.
fn random_animal(random_number: f64) -> Box<dyn Animal> {
    if random_number < 0.5 {
        Box::new(Sheep {})
    } else {
        Box::new(Cow {})
    }
}


let animal = random_animal(0.632);
println!("You've randomly chosen an animal, and it says {}", animal.noise());
```

A trait for a named tuple:

```rust
struct Pair(i32, i32);

trait Sum {
    fn sum(&self) -> i32;
}

impl Sum for Pair {
    fn sum(&self) -> i32 {
        self.0 + self.1
    }
}

let p = Pair(1,2);
p.sum()
```

```output
3
```

## Resources

* https://doc.rust-lang.org/rust-by-example/trait/dyn.html
