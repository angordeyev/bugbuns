---
draft: true
---

# loop

Return from loop:

```rust
let mut i = 1;

let l =
  loop {
      i = i + 1;

      if i == 3 {
          break i;
      }
  };

println!("{l}");
```

```output
3
```

