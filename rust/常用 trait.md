#rust

```rust
pub fn multipli(a: Matrix<T>, b: Matrix<T>) -> Result<Matrix<T>>
where
	// * 默认值 , Clone , 乘法 , += 加法 , 复制 的 Trait
	T: Default + Clone + Mul<Output = T> + AddAssign + Copy,
{
```
- `Default` 可以通过`T::default()` 获得当前类型的默认值
- `Mul<Output = T>` 乘法计算 , Output 设置计算结果类型
- `Add` 是加法 `AddAssign` 是使用`+=` 累加