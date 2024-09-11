#rust/crates #rust/key

这段代码展示了如何使用 Rust 中的 `jsonwebtoken` 库来创建和验证 JSON Web Tokens (JWT)。下面是代码的详细解释，包括每一行代码的作用和目的：

```rust

// 引入 jsonwebtoken 库中的错误类型
use jsonwebtoken::errors::ErrorKind;
// 引入 jsonwebtoken 库中用于创建和解码 JWT 的函数和结构体
use jsonwebtoken::{decode, encode, Algorithm, DecodingKey, EncodingKey, Header, Validation};
// 引入 serde 库中的 Serialize 和 Deserialize trait，用于序列化和反序列化 Rust 数据结构
use serde::{Deserialize, Serialize};

// 定义一个结构体 Claims，它将被用作 JWT 的有效载荷（payload）
// 这个结构体包含 JWT 的一些标准声明（claims），如 aud（受众）、sub（主题）、company（公司）和 exp（过期时间）
#[derive(Debug, Serialize, Deserialize)]
struct Claims {
    aud: String,  // 受众
    sub: String,  // 主题
    company: String,  // 公司名称
    exp: u64,  // 过期时间（Unix 时间戳）
}

fn main() {
    // 定义一个密钥，用于对 JWT 进行签名和验证
    let key = b"secret";
    // 创建一个 Claims 实例
    let my_claims = Claims {
        aud: "me".to_owned(),  // 设置受众为 "me"
        sub: "b@b.com".to_owned(),  // 设置主题为 "b@b.com"
        company: "ACME".to_owned(),  // 设置公司名称为 "ACME"
        exp: 10000000000,  // 设置过期时间为未来的某个时间点（Unix 时间戳）
    };
    // 使用 EncodingKey 和 Claims 来创建一个 JWT
    // 如果成功，将返回一个 token 字符串
    let token = match encode(&Header::default(), &my_claims, &EncodingKey::from_secret(key)) {
        Ok(t) => t,  // 如果 encode 函数成功，返回 token 字符串
        Err(_) => panic!(),  // 如果失败，在实践中应该返回错误信息，这里为了简单起见使用 panic
    };

    // 创建一个 Validation 实例，用于定义验证 JWT 时的规则
    let mut validation = Validation::new(Algorithm::HS256);
    // 设置验证规则，要求 JWT 的 sub（主题）声明必须为 "b@b.com"
    validation.sub = Some("b@b.com".to_string());
    // 设置验证规则，要求 JWT 的 aud（受众）声明必须包含 "me"
    validation.set_audience(&["me"]);
    // 设置验证规则，要求 JWT 必须包含 "exp", "sub", "aud" 这三个声明
    validation.set_required_spec_claims(&["exp", "sub", "aud"]);

    // 使用 DecodingKey 和之前定义的验证规则来解码并验证 JWT
    // 如果成功，将返回解码后的 Claims 和 Header
    let token_data = match decode::<Claims>(&token, &DecodingKey::from_secret(key), &validation) {
        Ok(c) => c,  // 如果 decode 函数成功，返回解码后的 Claims 和 Header
        Err(err) => match *err.kind() {
            // 如果错误类型是 InvalidToken，说明 token 本身无效
            ErrorKind::InvalidToken => panic!("Token is invalid"),
            // 如果错误类型是 InvalidIssuer，说明 token 的发行者无效
            ErrorKind::InvalidIssuer => panic!("Issuer is invalid"),
            // 其他类型的错误
            _ => panic!("Some other errors"),
        },
    };
    // 打印解码后的 Claims 和 Header，用于验证
    println!("{:?}", token_data.claims);
    println!("{:?}", token_data.header);
}
```