# CLI Tool

```shell
cargo new with-clap && cd $_
```

```shell
cargo add clap --features derive
```

```rust
use std::io::{stdin, BufRead, BufReader};

fn main() {
    let word_count = words_in_buf_reader(BufReader::new(stdin().lock()));
    println!("Words from {}", word_count)
}

fn words_in_buf_reader<R: BufRead>(buf_reader: R) -> usize {
    let mut count = 0;
    for line in buf_reader.lines() {
        count += line.unwrap().split(' ').count()
    }
    count
}
```
