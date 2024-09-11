#git #cliff 
## 规则配置

```toml
# cliff.toml
# # 解析和分组提交的正则表达式列表
commit_parsers = [
    { message = "\\[skip", skip = true },
    { message = "\\p{Han}", skip = true },
    { message = "^feat", group = "Features" },
    { message = "^fix", group = "Bug Fixes" },
    { message = "^doc", group = "Documentation" },
    { message = "^perf", group = "Performance" },
    { message = "^refactor", group = "Refactoring" },
    { message = "^style", group = "Style" },
    { message = "^revert", group = "Revert" },
    { message = "^test", group = "Tests" },
    { message = "^chore\\(version\\):", skip = true },
    { message = "^chore", group = "Miscellaneous Chores" },
    { message = ".*", group = "Other" },
    { body = ".*security", group = "Security" },
]
```

## 规则列表解释

1. 如果提交信息包含 `[skip]`，则跳过这条提交。
2. 如果提交信息包含任意汉字字符（`\p{Han}` 是 Unicode 汉字的正则表达式），则跳过这条提交。
3. 如果提交信息以 `feat` 开头，归入 "Features" 分组。
4. 如果提交信息以 `fix` 开头，归入 "Bug Fixes" 分组。
5. 如果提交信息以 `doc` 开头，归入 "Documentation" 分组。
6. 如果提交信息以 `perf` 开头，归入 "Performance" 分组。
7. 如果提交信息以 `refactor` 开头，归入 "Refactoring" 分组。
8. 如果提交信息以 `style` 开头，归入 "Style" 分组。
9. 如果提交信息以 `revert` 开头，归入 "Revert" 分组。
10. 如果提交信息以 `test` 开头，归入 "Tests" 分组。
11. 如果提交信息以 `chore(version):` 开头，跳过这条提交。
12. 如果提交信息以 `chore` 开头，归入 "Miscellaneous Chores" 分组。
13. 如果提交信息不匹配以上任何规则，归入 "Other" 分组。
14. 如果提交信息的正文包含 `security`，归入 "Security" 分组。
