#rust/crates #rust/web

- Axum

	- web 框架 Axum 是 tokio 团队开发的 , 完全支持 tower 生态

```shell
$ cargo add axum --features http2 --features query --features tracing
```

1. http2: 启用对 HTTP/2 协议的支持。这允许 Axum 应用使用更现代的 HTTP 协议特性，如头部压缩和多路复用。
2. query: 启用对 URL 查询字符串的解析支持。这使得从请求中解析查询参数变得更加方便。
3. tracing: 集成 tracing 日志框架，提供请求级别的日志记录和诊断信息。