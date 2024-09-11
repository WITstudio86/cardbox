#rust/tools 

## 安装与使用

```shell
$ brew install pre-commit
# 或者
$ pipx install pre-commit

# 使用之前需要在配置了.pre-commit-config.yaml的项目中进行初始话
$ pre-commit init
```


## 配置

可以使用pre-commit 进行提交前的自动检查

```yaml
# .pre-commit-config.yaml

# 如果检测到任何钩子失败，pre-commit 将不会继续执行剩余的钩子。
fail_fast: false

# repos 是一个钩子仓库的列表，每个仓库可以包含多个钩子。
repos:
  # 每个仓库通过 URL 指定，并且可以指定特定的版本（rev）。
  - repo: https://github.com/pre-commit/pre-commit-hooks 
    rev: v4.3.0
    hooks:
      # 这是从上述仓库中定义的钩子列表。
      - id: check-byte-order-marker   # 检查文件是否包含字节顺序标记（BOM）。
      - id: check-case-conflict       # 检查文件名在不同操作系统的大小写冲突。
      - id: check-merge-conflict     # 检查文件中是否有合并冲突。
      - id: check-symlinks           # 检查文件是否是符号链接。
      - id: check-yaml                # 检查 YAML 文件的格式。
      - id: end-of-file-fixer         # 确保文件以单个换行符结束。
      - id: mixed-line-ending        # 检查文件的行结束符是否一致。
      - id: trailing-whitespace      # 检查并修复行尾的空格。

  # 这是另一个仓库，用于 Python 代码格式化。
  - repo: https://github.com/psf/black 
    rev: 22.10.0
    hooks:
      - id: black  # 使用 Black 格式化 Python 代码。

  # local 部分定义了本地钩子。
  - repo: local
    hooks:
      # 每个钩子有以下属性：
      # id: 钩子的唯一标识符。
      # name: 钩子的名称。
      # description: 钩子的描述。
      # entry: 要执行的命令。
      # language: 钩子运行的语言环境。
      # files: 钩子应该运行的文件模式。
      # args: 传递给钩子的参数列表。
      # pass_filenames: 如果设置为 false，pre-commit 将不会传递文件名给钩子脚本。
      - id: cargo-fmt
        name: cargo fmt
        description: Format files with rustfmt.
        entry: bash -c 'cargo fmt -- --check'
        language: rust
        files: \.rs$  # 钩子仅对 Rust 源文件生效。
        args: []  # 不传递额外的参数。
```