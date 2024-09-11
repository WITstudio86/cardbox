
#rust/tools 

安装

```shell
# 拼写检查 typos
$ cargo install --locked cargo-typos
```

一般只需要配置忽略检查的文件

```toml
# _typos.rs
[default.extend-words]

[files]
extend-exclude = ["README.md", "LICENSECHANGELOG.md", "notebooks/*"]
```