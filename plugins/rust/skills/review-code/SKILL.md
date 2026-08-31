---
name: review-code
description: Review Rust code for correctness and style
when_to_use: When user asks to review code
disable-model-invocation: true
---

## 目的

按规则审查用户指定的代码内容

## 规则

* 若代码是作为一个模块，那么模块是否有对外暴露的 trait，而不是 impl；我希望调用方只关心 trait，因此 trait 必须存在
* 模块的核心代码与其单元测试代码，应以以下结构进行组织：
  ```
  src/
  foo/
    mod.rs       // 业务代码
    tests.rs     // 测试代码
  ```
* 模块内的每个 struct 都应该有单独的文件，而不是将所有代码都塞在同一个代码文件中
