# 02：连接 Obsidian 第二大脑

> 用途：让 Claude Code 创建一个 Obsidian 测试 vault，安装 MCPVault 连接，配置 Web Clipper 采集规则。
> 前置条件：已完成 `01-连接GitHub.md`。

---

## 给 Claude Code 的执行说明

请按顺序执行，不要跳步。

### 第 1 步：安装 MCPVault

检查：

```bash
which mcpvault
mcpvault --version
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
/Users/qiaozhanglong/Digital_Brain/乔帮主第二大脑配置包/Obsidian演示库
```

把用户确认的路径记为：

```text
VAULT_PATH
```

### 第 3 步：创建目录结构

在 `VAULT_PATH` 下创建：

```text
00-欢迎使用/
01-知识库/
02-课程素材/
03-案例展示/
04-执行记录/
05-模板/
06-系统设置/
.obsidian/
```

### 第 4 步：创建首页

在 vault 根目录创建 `index.md`：

```markdown
# 乔帮主第二大脑

这是乔帮主第二大脑配置包的 Obsidian 演示库。

它展示的是用户最终可以得到的第二大脑形态。

请在 Obsidian 中打开本目录，而不是上一级项目目录。

本库不等于乔帮主正式知识管理系统。

当前 vault 路径：

`VAULT_PATH`
```

### 第 5 步：创建 CLAUDE.md

在 vault 根目录创建 `CLAUDE.md`：

```markdown
# 我的第二大脑 — CLAUDE.md

## 关于我

- 这是我的 Obsidian 第二大脑测试库
- Claude Code 需要通过 MCP 管理这个 vault

## 目录结构

| 目录 | 用途 | 规则 |
|---|---|---|
| `00-欢迎使用/` | 入门引导和说明 | 只读为主 |
| `01-知识库/` | AI 消化后的结构化知识 | 可以新增、更新、建立链接 |
| `02-课程素材/` | 课程资料、讲义、测验 | NotebookLM 产物回写至此 |
| `03-案例展示/` | 案例和演示内容 | 用户可阅读和复制 |
| `04-执行记录/` | 执行日志和产物记录 | 每次执行后更新 |
| `05-模板/` | 模板 | 除非明确要求，不要随意修改 |
| `06-系统设置/` | 配置和设置 | 谨慎修改 |

## Claude Code 工作规则

- 用户说"消化知识库"时，读取 `01-知识库/`，提炼和整理。
- 每次新增知识库页面，都更新 `01-知识库/index.md` 和 `01-知识库/log.md`。
- NotebookLM、教学驾驶舱等产物，统一回写到 `02-课程素材/` 和 `04-执行记录/`。
- 不要删除用户原始资料。
```

### 第 6 步：创建 Claude Code 管理手册

在 vault 根目录创建 `Claude Code 管理手册.md`：

```markdown
# Claude Code 管理手册

## 知识库处理流程

当用户说"消化知识库"时：

1. 列出 `01-知识库/` 下所有文件。
2. 读取新增或未处理文件。
3. 按主题归类。
4. 为每个主题生成或更新 `01-知识库/主题.md`。
5. 更新 `01-知识库/index.md`。
6. 更新 `01-知识库/log.md`。
7. 生成 `04-执行记录/YYYY-MM-DD 知识重整.md`。

## 产物回写规则

最终成果放入 `02-课程素材/` 和 `04-执行记录/`，包括：

- 教学驾驶舱
- NotebookLM 信息图
- 简报
- 课程脚本
- 执行日志
```

### 第 7 步：创建知识库初始文件

创建 `01-知识库/index.md`：

```markdown
---
title: 知识库索引
type: index
updated: 2026-05-26
---

# 知识库索引

| 页面 | 一行摘要 |
|---|---|
| （等待第一次知识重整） | |
```

创建 `01-知识库/log.md`：

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

### 第 8 步：连接 Claude Code MCP

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
obsidian-secondbrain ... Connected
```

如果显示连接失败，先用 MCPVault 本地测试：

```bash
echo '{"jsonrpc":"2.0","id":1,"method":"tools/list"}' | mcpvault "VAULT_PATH"
```

如果能返回工具列表，说明 MCPVault 正常，问题在 Claude Code 配置加载，重启 Claude Code 再检查。

### 第 9 步：安装和设置 Obsidian Web Clipper

请告诉用户：

```text
网页内容通常由 Obsidian Web Clipper 浏览器插件采集。
```

用户需要手动完成：

1. 打开 Chrome Web Store。
2. 搜索并安装 `Obsidian Web Clipper`。
3. 打开任意网页，点击浏览器右上角 Web Clipper 图标。
4. 设置：

```text
Vault: 当前 secondbrain vault
Folder / Location: 01-知识库
```

建议模板字段包含：

```markdown
---
title: "{{title}}"
source: "{{url}}"
clipped: "{{date}}"
type: clipping
tags:
  - clipping
---

# {{title}}

原文链接：{{url}}

{{content}}
```

这样用户回到 Obsidian 后，就能在 `01-知识库/` 看到这篇网页剪藏。

如果想回到原网页，打开剪藏笔记里的 `原文链接` 即可。

### 第 10 步：提醒用户重启 Claude Code

告诉用户：

```text
Claude Code 已经连接 Obsidian 第二大脑。
请重启 Claude Code，让新的 MCP 工具生效。
重启后可以说："读取 obsidian-secondbrain，消化知识库。"
```

---

## 用户怎么采集网页内容？

推荐方式：安装 Obsidian Web Clipper 浏览器插件。

设置：

```text
Vault: 这个 secondbrain vault
Folder: 01-知识库
```

以后看到网页，点击浏览器插件，它会把网页保存成 Markdown 文件，进入：

```text
01-知识库/
```

Claude Code 再负责把 `01-知识库/` 消化整理。

补充：

- 网页文章：用 Obsidian Web Clipper。
- YouTube 视频：下载字幕或转写成 Markdown，放进 `01-知识库/`。
- PDF / 课程稿：先提取成 Markdown，放进 `01-知识库/`。
- NotebookLM 生成物：下载后写入 `02-课程素材/`，不是放进 `01-知识库/`。

---

## 下一步

Obsidian 连接完成后，继续读取 `03-连接NotebookLM课程素材工厂.md`。
