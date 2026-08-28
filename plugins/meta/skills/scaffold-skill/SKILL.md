---
name: scaffold-skill
description: Scaffold a new skill template under an existing or new plugin.
when_to_use: When the user asks to create, scaffold, or add a new skill.
argument-hint: <skill-name>
arguments: skill_name
disable-model-invocation: true
---

根据用户提供的 skill 名称（`$skill_name`），在本仓库中创建一个 skill 模版。

## 步骤

### 1. 验证 skill 名称

从参数获取 skill 名称，确保为 kebab-case 格式（小写字母、数字、连字符）。若格式不符，自动转换并告知用户。

### 2. 选择目标 plugin

读取 `.claude-plugin/marketplace.json`，列出当前所有已注册的 plugin，让用户选择将 skill 添加到哪个 plugin 下；同时提供「创建新 plugin」的选项。

若用户选择创建新 plugin：
* 询问 plugin 名称（kebab-case）和描述
* 创建 `plugins/<plugin-name>/.claude-plugin/plugin.json`，内容：
  ```json
  {
    "name": "<plugin-name>",
    "description": "<plugin 描述>",
    "version": "0.0.1"
  }
  ```
* 在 `.claude-plugin/marketplace.json` 的 `plugins` 数组中注册新 plugin，格式：
  ```json
  {
    "name": "<plugin-name>",
    "source": "./plugins/<plugin-name>",
    "description": "<plugin 描述>"
  }
  ```

### 3. 收集 skill 配置

向用户询问以下信息：

1. **description** — skill 的功能描述（必填；description + when_to_use 合计不超过 1536 字符）
2. **when_to_use** — 何时触发此 skill（选填）
3. **调用方式** — 询问用户此 skill 的调用权限，解释以下三种模式的含义后让用户选择：
   * **仅用户调用**（`disable-model-invocation: true`）— Claude 不会自动加载此 skill，只能通过 `/name` 手动调用
   * **仅模型调用**（`user-invocable: false`）— 不出现在 `/` 菜单中，只能由 Claude 根据上下文自动调用
   * **均可调用**（两个字段均为默认值，无需写入）— 用户可通过 `/name` 调用，Claude 也可自动调用
4. **argument-hint** — 是否需要参数提示（选填，如 `[issue-number]`、`[filename]`）

### 4. 创建 SKILL.md

在目标 plugin 下创建 `skills/<skill-name>/SKILL.md`。

根据用户在步骤 3 中的选择，生成对应的 frontmatter。规则：
* 始终包含 `name` 和 `description`
* 仅当用户提供了 `when_to_use` 时才写入该字段
* 仅当用户提供了 `argument-hint` 时才写入该字段
* 调用方式：
  * 仅用户调用 → 写入 `disable-model-invocation: true`
  * 仅模型调用 → 写入 `user-invocable: false`
  * 均可调用 → 不写入这两个字段
* 不写入值为默认值的字段，保持 frontmatter 简洁

模版示例（仅用户调用、有参数提示）：

```markdown
---
name: <skill-name>
description: <用户提供的描述>
when_to_use: <用户提供的触发条件>
argument-hint: <用户提供的参数提示>
disable-model-invocation: true
---

<在此编写 skill 的具体指令>
```

### 5. 完成提示

创建完成后：
* 显示生成文件的路径
* 显示 skill 的调用方式（如 `/<plugin-name>:<skill-name>`）
* 提醒用户编辑 SKILL.md body 部分，填写具体的 skill 指令
* 提示可通过 `claude plugin validate ./plugins/<plugin-name>` 验证 plugin 结构
