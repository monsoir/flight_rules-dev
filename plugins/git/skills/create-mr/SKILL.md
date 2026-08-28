---
name: create-mr
description: Generate a Merge Request from local changes.
when_to_use: When the user asks to create a MR, merge request, or submit local changes for review.
disable-model-invocation: true
---

根据本地修改生成一个 Merge Request ，要求：
* 根据 remote 的地址，使用响应的 CLI 工具操作，如 `gh` ， `glab`
* 默认向主分支（一般为 `main` 或 `master` 分支）发起 Merge Request
* Merge Request 中清晰地描述以下内容：
  * 此 Merge Request 的总体内容
  * 每一个部分修改的原因及其内容
  * 测试内容以及测试结果
