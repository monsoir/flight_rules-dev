---
name: create-tag
description: Create and push a git tag.
argument-hint: "[tag-name]"
disable-model-invocation: true
---

用户通过参数提供 tag 名称（即 `[tag-name]`）。若用户未提供，则询问用户。

1. 确认当前处于主分支（main 或 master）并拉取最新代码。若不在主分支上，中止操作并告知用户只允许在主分支上打 tag
2. 检查是否存在 tag 推送后的自动化触发配置（检查 `.github/workflows/*` 中的 `on.push.tags`、`.gitlab-ci.yml` 中的 `tags:` 等）。若未找到相关配置，提醒用户当前没有 tag 触发的自动化流程
3. 创建 git tag；需要先检查 remote 是否有同名 tag，若有则失败报错
4. 将 tag 推送到 remote
