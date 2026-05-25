# Claude Code Starter Kit 01：建立第二大脑

> 用途：让 Claude Code 自动创建一个 Obsidian 测试 vault，并通过 MCPVault 学会读写这个知识库。
> 适用对象：想复刻三师爸“AI 第二大脑 + 教学驾驶舱”流程的人。

---

## 这个懒人包会帮你做什么？

完成后，你会得到：

- 一个新的 Obsidian 测试 vault
- 标准目录结构：`Clippings`、`知识库`、`创作库`、`每日笔记`、`Templates`
- 一个 `CLAUDE.md`，告诉 Claude Code 怎么管理这个 vault
- 一个 `Claude Code 管理手册.md`
- MCPVault 连接，让 Claude Code 可以读写 Obsidian 文件

默认测试 vault 路径：

```text
/Users/qiaozhanglong/ Digital_Brain/三师爸原版复刻实验/secondbrain
```

如果你不是乔帮主本人，请让 Claude Code 先询问你想把 vault 放在哪里。

---

## 给 Claude Code 的执行说明

下面的内容是给 Claude Code 读的。请 Claude Code 按顺序执行，不要跳步。

### 第 1 步：检查环境

请检查：

```bash
git --version
node --version
npm --version
claude --version
```

如果 `mcpvault` 不存在，执行：

```bash
npm install -g @bitbonsai/mcpvault
```

安装后确认：

```bash
which mcpvault
mcpvault --version
```

### 第 2 步：确认 vault 路径

询问用户：

```text
你要把测试 Obsidian vault 放在哪里？
如果你没有特别要求，我将使用：
/Users/qiaozhanglong/ Digital_Brain/三师爸原版复刻实验/secondbrain
```

把用户确认的路径记为：

```text
VAULT_PATH
```

### 第 3 步：创建目录结构

在 `VAULT_PATH` 下创建：

```text
Clippings/
知识库/
创作库/
每日笔记/
Templates/
.obsidian/
```

### 第 4 步：创建 CLAUDE.md

在 vault 根目录创建 `CLAUDE.md`：

```markdown
# 我的第二大脑 — CLAUDE.md

## 关于我

- 这是我的 Obsidian 第二大脑测试库
- Claude Code 需要通过 MCP 管理这个 vault

## 目录结构

| 目录 | 用途 | 规则 |
|---|---|---|
| `Clippings/` | 原始输入 | 只读为主，不改原文 |
| `知识库/` | AI 消化后的结构化知识 | 可以新增、更新、建立链接 |
| `创作库/` | 可交付产物 | 存课程、网页、信息图、交付记录 |
| `每日笔记/` | 日志和周报 | 存知识重整记录 |
| `Templates/` | 模板 | 除非明确要求，不要随意修改 |

## Claude Code 工作规则

- 用户说“消化 Clippings”时，读取 `Clippings/`，提炼到 `知识库/`。
- 每次新增知识库页面，都更新 `知识库/index.md` 和 `知识库/log.md`。
- NotebookLM、GitHub Pages、教学驾驶舱等产物，统一回写到 `创作库/`。
- 不要删除用户原始资料。
```

### 第 5 步：创建 Claude Code 管理手册

在 vault 根目录创建 `Claude Code 管理手册.md`：

```markdown
# Claude Code 管理手册

## Clippings 处理流程

当用户说“消化 Clippings”时：

1. 列出 `Clippings/` 下所有文件。
2. 读取新增或未处理文件。
3. 按主题归类。
4. 为每个主题生成或更新 `知识库/主题.md`。
5. 更新 `知识库/index.md`。
6. 更新 `知识库/log.md`。
7. 生成 `每日笔记/YYYY-MM-DD 知识重整.md`。

## 产物回写规则

最终成果放入 `创作库/`，包括：

- 教学驾驶舱
- NotebookLM 信息图
- 简报
- GitHub Pages 页面
- 课程脚本
```

### 第 6 步：创建知识库初始文件

创建 `知识库/index.md`：

```markdown
---
title: 知识库索引
type: index
updated: 2026-05-25
---

# 知识库索引

| 页面 | 一行摘要 |
|---|---|
| （等待第一次知识重整） | |
```

创建 `知识库/log.md`：

```markdown
---
title: 知识库操作记录
type: log
---

# 知识库操作记录

## 初始化

- 创建第二大脑目录结构
- 创建 Claude Code 管理规则
```

### 第 7 步：连接 Claude Code MCP

执行：

```bash
claude mcp add --scope user obsidian-secondbrain -- mcpvault "VAULT_PATH"
```

如果 `mcpvault` 不在 PATH 中，用 `which mcpvault` 得到完整路径，例如：

```bash
claude mcp add --scope user obsidian-secondbrain -- /Users/qiaozhanglong/.npm-global/bin/mcpvault "VAULT_PATH"
```

然后检查：

```bash
claude mcp list
```

必须看到：

```text
obsidian-secondbrain ... ✓ Connected
```

### 第 8 步：提醒用户重启 Claude Code

告诉用户：

```text
Claude Code 已经连接 Obsidian 第二大脑。
请重启 Claude Code，让新的 MCP 工具生效。
重启后可以说：“读取 obsidian-secondbrain，消化 Clippings。”
```

---

## 用户怎么采集 Clippings？

推荐方式：安装 Obsidian Web Clipper 浏览器插件。

设置：

```text
Vault: 这个 secondbrain vault
Folder: Clippings
```

以后看到网页，点击浏览器插件，它会把网页保存成 Markdown 文件，进入：

```text
Clippings/
```

Claude Code 再负责把 `Clippings/` 消化到 `知识库/`。
