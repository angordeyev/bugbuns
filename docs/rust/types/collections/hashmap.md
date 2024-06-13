---
draft: true
---

# HashMap

An example:

```rust
use std::collections::HashMap;

let mut dict: HashMap<&str, u8> = HashMap::new();

dict.insert("hello", 1);

println!("{}", dict["hello"]);
```

```output
1
```
