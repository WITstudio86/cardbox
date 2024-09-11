#rust/crates #rust/web

异步实现库 , rust 只提供了异步需要的类型等 , 库可以自由选择

```
# full features 是安装所有 freatures
# 
cargo add tokio --features rt --features rt-multi-thread --features macros --features net --features fs
```

1. `rt`: 这是 Tokio 的异步运行时。这是 Tokio 的核心功能，它提供了异步任务的执行和管理。如果你想要使用 Tokio 的异步编程特性，你需要启用这个功能。
2. `rtmulti-thread`: 这个功能启用了多线程运行时。默认情况下，Tokio 的运行时是单线程的，这意味着所有的异步任务都在同一个线程上执行。启用 `rtmulti-thread` 功能后，Tokio 将使用一个线程池来执行任务，这可以提高并发性能。
3. `macros`: 这个功能提供了 Tokio 的宏支持。Tokio 有一些特定的宏，比如 `#[tokio::main]`，它用于标记异步的主函数。启用这个功能后，你就可以在你的代码中使用这些宏。
4. `net`: 这个功能启用了网络相关的组件。如果你需要使用 Tokio 提供的 TCP/UDP 网络功能，比如创建异步的 TCP 服务器或客户端，你需要启用这个功能。
5. `fs`: 这个功能提供了文件系统相关的异步操作。如果你需要异步地读写文件，或者执行其他文件系统操作，比如获取文件的元数据，你需要启用这个功能。