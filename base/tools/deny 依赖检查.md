#rust/tools

依赖安全性检查 , 主要是通过 `allow=[]`字段检查所使用的依赖 , 例如闭源的商业代码不能使用要求开源的依赖

```shell
# 下载
$ cargo install cargo-deny
# 到项目中初始化 deny.toml 文件
$ cargo deny init
# 运行检查
$ cargo deny check
```

`cargo deny init` 会在 deny.toml 中生成缺省的配置文件

```toml
# deny.toml
allow = [
  "MIT",
  "Apache-2.0",
  "Unicode-DFS-2016",
  "MPL-2.0",
  "BSD-2-Clause",
  "BSD-3-Clause",
  "ISC",
  "CC0-1.0",
]
```
