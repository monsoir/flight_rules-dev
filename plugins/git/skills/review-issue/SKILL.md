---
name: review-issue
description: Review issue solutions on GitHub or GitLab with a specified model
when_to_use: When the user manually invokes this skill to review an issue
argument-hint: "[model-name]"
disable-model-invocation: true
---

使用用户指定的模型审查给出的 issue

## 要求

* 根据 issue 地址，判断 issue 所托管的平台，进而决定使用相应的 CLI 工具，如 `gh`, `glab`
* 依据审查结果，对每一项建议或问题，逐项向用户询问与解释，不能一次性地将所有内容输出

## 审查内容

包括但不限于：
* 数据安全（是否容易被攻击）
* API 设计是否足够明确清晰、易用

## 询问行文

* 简介问题或建议的主要内容，修改点、风险
* 再详细展开问题或建议的细节
