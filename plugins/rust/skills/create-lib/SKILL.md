---
name: create-lib
description: Create a new Rust crate (library or binary) with this workspace's conventions.
when_to_use: When the user asks to add a crate, new lib, new binary, or scaffold a Rust package.
disable-model-invocation: true
---

创建一个 Rust 语言的 lib 项目框架，要点：
* 禁止使用 `unsafe`
* 使用 `just` 作自动化任务管理
* 搭建 CI/CD 流程，要求：
  * 各模块的单元测试必须通过
  * 不能有任何编译警告
  * lib 的版本号通过 CI 对接 git tag
