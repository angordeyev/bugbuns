---
draft: true
---

# Enum

```rust
enum Message {
   Paused(bool),
   Echo(String),
}

let message = Message::Paused(true);

match message {
    Message::Paused(paused) => println!("Paused: {paused}"),
    Message::Echo(text) => println!("Message: {text}")
}
```

```output
Paused: true
```

```rust
use Message::*;

enum Message {
   Paused(bool),
   Echo(String),
}

let message = Paused(true);

match message {
    Paused(paused) => println!("Paused: {paused}"),
    Echo(text) => println!("Message: {text}")
}
```

```output
Paused: true
```

## Resources

* [How to match an enum variant in a match](https://stackoverflow.com/questions/70962624/how-to-match-an-enum-variant-in-a-match)
