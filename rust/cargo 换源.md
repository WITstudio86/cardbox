#rust/crates 

大多数源只是换了索引源 , 内部依赖还是从 crates.io 访问 , 下面这个可以

编辑或创建 `$CARGO_HOME/config.toml` 文件（其中`$CARGO_HOME`通常是`$HOME/.cargo`），内容如下：

```toml
[source.crates-io]   
replace-with = "ustc"      
[source.ustc]   
registry = "sparse+https://mirrors.ustc.edu.cn/crates.io-index/"   
```

其中"sparse+"表示使用稀疏索引镜像，性能更佳，适用Rust 1.68及以上版本（当前最新版本已经是1.78）。如上文所述，中国科学技术大学USTC镜像支持通过国内链接下载crate包，不受境外链接所限。  
  

来自: [Rust更换Cargo国内源，镜像了寂寞（更新：不再寂寞）_rust 国内源-CSDN博客](https://blog.csdn.net/liigo/article/details/132814673)