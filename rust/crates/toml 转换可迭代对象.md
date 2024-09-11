注意 toml 不能转换由可转换数据类型组成的可迭代对象 , 需要循环遍历

```rust
let mut content = String::new();
let mut n = 1;
for record in records {
    content.push_str(format!("[record{}]\n", n).as_str());
    content.push_str(toml::to_string(&record)?.as_str());
    n += 1;
}
content
```