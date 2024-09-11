#rust/thread

```rust
pub fn spawn<F, T>(f: F) -> JoinHandle<T>
where
    F: FnOnce() -> T + Send + 'static,
    T: Send + 'static,
```

- `FnOnce() -> T` trait 约束了是一个只执行一次的闭包函数
- `Send` 实现了这个 trait 的数据可以在线程中移动
- `'static` 拥有静态生命周期 , 也间接要求了需要是owned数据

> `spawn` 可以创建一个线程 , 主线程并不会等待子线程运行完毕 , 如果主线程结束会自动释放子线程 , 需要通过`.join()` 控制在主线程的某个地方等待子线程执行结束并返回结果