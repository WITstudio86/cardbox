当一个错误通过 `?`向外传递的时候如果不可以自动转换 , 可以通过 `err_map`将其变为一个由 anyhow 构建的错误

```rust
use anyhow;
fn main() -> anyhow::Result<()> {
    let thread = std::thread::spawn(|| {
        println!("Hello from thread!");
    });

    thread.join()?;
    Ok(())
}
```

> 上面代码中的`thread.join()?;` 会报错 , 因为其返回的错误并不能够自动转换为 anyhow::Result

需要将`thread.join()?;` 返回的 Result中的错误 处理为 anyhow 可以处理的错误

```rust
use anyhow::anyhow;
fn main() -> anyhow::Result<()> {
    let thread = std::thread::spawn(|| {
        println!("Hello from thread!");
    });

    // thread.join()?;
    thread
        .join()
        // 通过 map_err 将错误转换为 anyhow::Error 类型
        .map_err(|e| anyhow!("Error joining thread: {:?}", e))?;
    Ok(())
}

```