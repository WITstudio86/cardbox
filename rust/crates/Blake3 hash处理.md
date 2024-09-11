#rust/crates #rust/key 

做文本哈希 , 可以实现 keyed_hase 已有的共有 key 实现编解码 hash

```rust
// 通过已有键试下你 keyed hash 的实例
impl TextSign for Blake3 {
    fn textsign(&self, data: String) -> anyhow::Result<String> {
        let data = data.as_bytes();
        let signture = blake3::keyed_hash(&self.key, data);
        Ok(signture.to_string())
    }
}
```

验证就是从新根据内容生成 hash 比较 hash 即可