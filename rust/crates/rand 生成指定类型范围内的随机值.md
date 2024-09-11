#rust/crates 

```rust
use rand;
fn main() {
    let randi32 = rand::random::<i32>();
    // 生成 u64类型的 u8 范围内的随机数
    let randu8 = rand::random::<u8>() as u64;
}

```