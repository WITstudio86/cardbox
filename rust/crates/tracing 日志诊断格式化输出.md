#rust/crates #rust/web

- tracing
- tracing_subscriber

- `tracing_subscriber::fmt::init()` 是 Rust 语言中 tracing 库的一个函数，用于初始化和配置 tracing 的格式化和输出。tracing 是 Rust 的一个流行的日志和诊断集合，它提供了一种灵活的方式来收集和输出应用程序的运行时信息。
- `tracing_subscriber::fmt::init()` 是 Rust 语言中 tracing 库的一个函数，用于初始化和配置 tracing 的格式化和输出。tracing 是 Rust 的一个流行的日志和诊断集合，它提供了一种灵活的方式来收集和输出应用程序的运行时信息。

```shell
$ cargo add tracing
$ cargo add tracing_subscriber --features env-filter
```

之后再主函数中调用 `tracing_subscriber::fmt::init()`完成初始化及配置 , 就可以通过 `RUST_LOG=debug cargo run`执行程序 , 将tracing 输出打印到 console

- `info!()`