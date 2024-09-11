#rust/crates 

如果希望给一个枚举中的多个类型实现相同的 trait , 执行实例中的具体方法,

例如下面代码中的 FlagEnum 就是一个 enum , 其中的 FlagStruct1 和 FlagStruct2 都实现了 Flag 这个 trait , 但是不可以直接使用 `flag.flag()`方法 , 因为实例的类型是枚举 ,

但是此处不管 math 的是谁 , 我都会执行 trait 中的 flag 方法 , 就可以使用 enum_dispatch 简化

```rust
trait Flag {
    fn flag(&self) -> ();
}

enum FlagEnum {
    Flag1(FlagStruct1),
    Flag2(FlagStruct2),
}

struct FlagStruct1;
struct FlagStruct2;

impl Flag for FlagStruct1 {
    fn flag(&self) -> () {
        println!("Flag 1 is true")
    }
}

impl Flag for FlagStruct2 {
    fn flag(&self) -> () {
        println!("Flag 2 is false")
    }
}

fn main() {
    let flag = FlagEnum::Flag1(FlagStruct1);
    // flag.flag();
    // ↑ 错误的 调用方式 因为flag是一个enum，需要使用match来调用
    match flag {
        FlagEnum::Flag1(f) => f.flag(),
        FlagEnum::Flag2(f) => f.flag(),
    }
}
```

使用 enum_dispatch 的优化方式:

```rust
use enum_dispatch::enum_dispatch;

#[enum_dispatch]
trait Flag {
    fn flag(&self) -> ();
}

#[enum_dispatch(Flag)]
enum FlagEnum {
    Flag1(FlagStruct1),
    Flag2(FlagStruct2),
}

struct FlagStruct1;
struct FlagStruct2;

impl Flag for FlagStruct1 {
    fn flag(&self) -> () {
        println!("Flag 1 is true")
    }
}

impl Flag for FlagStruct2 {
    fn flag(&self) -> () {
        println!("Flag 2 is false")
    }
}

fn main() {
    let flag = FlagEnum::Flag1(FlagStruct1);
    flag.flag();
}
```

注意

1. 当跨文件使用 trait 中规定的方法的时候 需要先导入 trait 到当前 scop 中才可以生效