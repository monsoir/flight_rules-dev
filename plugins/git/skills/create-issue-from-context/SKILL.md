---
name: create-issue-from-context
description: Create a GitHub/GitLab issue from the current context
when_to_use: When the user wants to report a bug or request a feature
argument-hint: "[bug|feature|improvement]"
disable-model-invocation: true
---

## 流程

根据会话的上下文，创建一个 issue ，要求：
* 提交 issue 时，根据 git remote 使用相应的 CLI，如 `gh` 、`glab`
* 编写 issue 时，必须包含 title 与 body，其中：
  * title 必须以简洁的形式描述出 issue 的目标
  * body 的格式需符合下文中提及的模版
* issue 创建成功后回显链接

## Issue body 模版

根据参数指定的类型，使用对应的模版。

### Bug

```markdown
## 概括

<描述问题现象，200 字内>

## 复现步骤

<分点列出可复现的最小步骤>

## 预期行为与实际行为

* 预期：<预期的正确行为>
* 实际：<当前的错误行为>

## 原因分析

<若上下文已定位成因则填写并标注相关代码位置；否则标注为「待排查」或省略本节>

## 验收标准

<描述验证 bug 已修复的测试条件，明确边界情况>
```

### Feature

```markdown
## 概括

<描述需求目标，200 字内>

## 背景与动机

<当前的问题或限制，为何需要此 feature>

## 方案设想

<分点描述预期的实现方式及各部分的理由；不确定处标注为待讨论>

## 验收标准

<分点列出可验证的完成条件，明确边界情况>
```

### Improvement

```markdown
## 概括

<描述改进目标，200 字内>

## 现状与不足

<当前实现的问题，如性能瓶颈、可读性差、维护成本高等>

## 改进方案

<分点描述改进措施及预期效果>

## 验收标准

<分点列出可验证的完成条件，明确边界情况>
```
