---
name: merge-mr
description: Merge a known Merge Request from the current conversation.
when_to_use: When the user asks to merge a MR or merge request that has already been discussed in the conversation.
disable-model-invocation: true
---

合并对话内已知的 Merge Request ，要求：
* 使用 `glab` 操作
* 若对话内没有已知的 MR，则停止操作
