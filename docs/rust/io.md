---
draft: true
---

# io

## Files

Read a file:

```rust
{
    use std::fs;
    let text = fs::read_to_string(file_path)?;
    print!("{text}");
}
```

Read from STDIN:

```rust
use std::io;

fn main() -> io::Result<()>{
    let stdin = io::read_to_string(io::stdin())?;
    println!("Stdin was:");
    println!("{stdin}");
    Ok(())
}
```
