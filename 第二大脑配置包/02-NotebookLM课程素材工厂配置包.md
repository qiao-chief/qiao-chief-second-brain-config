# 乔帮主第二大脑配置包 02：NotebookLM 课程素材工厂

> 用途：让 Claude Code 使用 NotebookLM，把一批课程资料、网页、PDF、YouTube 字幕或旧讲义，转成可复用的课程素材，并回写到 Obsidian 第二大脑。
> 前置条件：已经完成 `01-第二大脑配置包.md`，Claude Code 已连接 `obsidian-secondbrain`，NotebookLM CLI 已登录。

---

## 乔帮主欢迎语

你好，我是乔帮主。

如果第一个配置包解决的是“让 AI 认识你”，那这个配置包解决的就是“让 AI 开始替你干活”。

你不需要一页页重做课件，也不需要从空白文档开始写课程。你只要把旧资料、外网素材、PDF、网页、视频字幕放进来，Claude Code 会调用 NotebookLM 帮你消化，再把简报、信息图、讲义、测验和产物记录整理回你的第二大脑。

从这一刻开始，你的资料不只是资料，而是可以被加工、组合、交付的课程资产。

---

## 这个配置包会帮你做什么？

完成后，你会得到一套“课程素材工厂”：

- 一个 NotebookLM notebook
- 一批已上传的 source
- 一份课程素材分析报告
- 一份授课简报
- 一张或多张信息图
- 一份课程讲义草稿
- 一份基础测验题
- 一个 Obsidian 产物记录页
- 一个本地下载目录

默认输出位置：

```text
/Users/qiaozhanglong/ Digital_Brain/Qiao-Second-Brain/创作库/课程素材工厂/
```

如果用户使用别的 vault，请 Claude Code 先询问实际路径。

---

## 给 Claude Code 的执行说明

下面的内容是给 Claude Code 读的。请按顺序执行。

### 第 0 步：确认目标

先问用户三个问题：

```text
1. 这次要加工的课程主题是什么？
2. 原始资料放在哪里？可以是文件夹、PDF、Markdown、网页链接或 YouTube 链接。
3. 你希望产出什么？默认：简报、信息图、讲义、测验、Obsidian 记录。
```

将答案记为：

```text
COURSE_TOPIC
SOURCE_PATH_OR_URLS
OUTPUT_REQUIREMENTS
```

如果用户没有指定课程主题，Claude Code 根据资料内容自动命名。

### 第 1 步：检查前置环境

检查：

```bash
claude --version
nlm --version
nlm doctor
```

必须满足：

```text
NotebookLM 已登录
Claude Code 已能连接 notebooklm-mcp
Claude Code 已能连接 obsidian-secondbrain
```

验证 Claude Code MCP：

```bash
claude mcp list
```

必须看到：

```text
notebooklm-mcp ... ✓ Connected
obsidian-secondbrain ... ✓ Connected
```

如果 NotebookLM 未登录：

```bash
nlm login
```

请暂停，让用户在 Chrome 中完成 Google 登录。

### 第 2 步：准备项目目录

创建本地工作目录：

```bash
mkdir -p "$HOME/Documents/Qiao-Course-Material-Factory"
```

在其中为本次主题创建子目录。目录名使用英文或拼音 kebab-case。

示例：

```text
$HOME/Documents/Qiao-Course-Material-Factory/triangle-angle-sum/
```

目录结构：

```text
主题目录/
├── sources/          原始资料副本或清单
├── downloads/        NotebookLM 下载产物
├── notes/            Claude Code 整理后的中间稿
└── output/           可交付成品
```

### 第 3 步：创建 NotebookLM notebook

执行：

```bash
nlm notebook create "COURSE_TOPIC"
```

记录返回的 notebook ID：

```text
NOTEBOOK_ID
```

### 第 4 步：添加资料源

根据资料类型选择。

**本地 PDF / 文件：**

```bash
nlm source add NOTEBOOK_ID --file "文件路径" --wait --wait-timeout 300
```

**网页链接：**

```bash
nlm source add NOTEBOOK_ID --url "网页链接" --wait --wait-timeout 300
```

**YouTube 链接：**

```bash
nlm source add NOTEBOOK_ID --youtube "YouTube链接" --wait --wait-timeout 300
```

**纯文本 / Markdown：**

```bash
nlm source add NOTEBOOK_ID --title "资料标题" --text "资料内容" --wait --wait-timeout 300
```

如果资料很多，先控制在 3-7 个 source，避免第一次测试过大。

### 第 5 步：生成课程素材分析报告

先让 NotebookLM 描述资料：

```bash
nlm notebook describe NOTEBOOK_ID
```

如果 `notebook describe` 不可用，使用：

```bash
nlm query NOTEBOOK_ID "请基于当前资料，整理课程主题、目标学员、核心模块、关键概念、案例、可做成练习的问题。"
```

将结果保存到：

```text
notes/课程素材分析.md
```

报告结构：

```markdown
# 课程素材分析

## 课程主题

## 目标学员

## 核心模块

## 关键概念

## 可用案例

## 可设计练习

## 缺口和待补资料
```

### 第 6 步：生成 NotebookLM 产物

默认生成四类产物。

**1. 授课简报**

```bash
nlm slides create NOTEBOOK_ID \
  --format detailed_deck \
  --length default \
  --language zh-CN \
  --focus "围绕 COURSE_TOPIC 生成一份适合课堂讲授或训练营讲解的详细简报，包含结构、关键概念、案例、练习和总结。" \
  --confirm
```

**2. 信息图**

```bash
nlm infographic create NOTEBOOK_ID \
  --orientation landscape \
  --detail detailed \
  --style sketch_note \
  --language zh-CN \
  --focus "围绕 COURSE_TOPIC 生成一张适合课程讲解的手绘信息图，突出核心模型、流程和常见错误。" \
  --confirm
```

**3. 课程讲义报告**

```bash
nlm report create NOTEBOOK_ID \
  --language zh-CN \
  --focus "基于资料生成一份课程讲义草稿，要求结构清晰，适合学员课后复习。" \
  --confirm
```

如果 `report create` 参数不兼容，先执行：

```bash
nlm report create --help
```

再按本机 CLI 提示调整。

**4. 测验题**

```bash
nlm quiz create NOTEBOOK_ID \
  --question-count 10 \
  --difficulty medium \
  --language zh-CN \
  --focus "围绕 COURSE_TOPIC 生成 10 道理解和应用题，帮助学员自测。" \
  --confirm
```

如果 `quiz create` 参数不兼容，先执行：

```bash
nlm quiz create --help
```

再按本机 CLI 提示调整。

### 第 7 步：等待生成完成

轮询：

```bash
nlm studio status NOTEBOOK_ID
```

每 60 秒检查一次，直到需要的产物为：

```text
completed
```

如果某个产物长期 `in_progress` 超过 15 分钟，记录到 `notes/执行日志.md`，先下载已完成产物。

### 第 8 步：下载产物

下载到：

```text
downloads/
```

示例：

```bash
nlm download infographic NOTEBOOK_ID --output "downloads/信息图.png"
nlm download slide-deck NOTEBOOK_ID --output "downloads/授课简报.pdf"
nlm download report NOTEBOOK_ID --output "downloads/课程讲义.md"
nlm download quiz NOTEBOOK_ID --output "downloads/测验题.json"
```

如果命令参数不兼容，先执行：

```bash
nlm download --help
nlm download infographic --help
nlm download slide-deck --help
nlm download report --help
nlm download quiz --help
```

按本机版本调整。

### 第 9 步：整理本地产物

将下载物整理到：

```text
output/
```

建议命名：

```text
COURSE_TOPIC-课程素材分析.md
COURSE_TOPIC-授课简报.pdf
COURSE_TOPIC-信息图.png
COURSE_TOPIC-课程讲义.md
COURSE_TOPIC-测验题.json
COURSE_TOPIC-执行日志.md
```

如果信息图要用于网页，额外转成 JPG：

```bash
sips -s format jpeg -z 1080 1920 "downloads/信息图.png" --out "output/信息图.jpg"
```

### 第 10 步：回写 Obsidian 第二大脑

将产物记录写入：

```text
创作库/课程素材工厂/COURSE_TOPIC.md
```

如果目录不存在，先创建：

```text
创作库/课程素材工厂/
```

产物记录模板：

```markdown
---
title: COURSE_TOPIC 课程素材工厂记录
date: YYYY-MM-DD
type: 课程素材工厂
source: NotebookLM
tags:
  - NotebookLM
  - 课程素材
  - 第二大脑
---

# COURSE_TOPIC 课程素材工厂记录

## 输入资料

- source 1
- source 2

## NotebookLM Notebook

- Notebook ID: NOTEBOOK_ID

## 生成产物

| 类型 | 文件 | 状态 |
|---|---|---|
| 课程素材分析 |  | 已完成 |
| 授课简报 |  | 已完成 |
| 信息图 |  | 已完成 |
| 课程讲义 |  | 已完成 |
| 测验题 |  | 已完成 |

## 课程结构初稿

## 可直接使用的内容

## 待人工判断的问题

## 下一步建议
```

同时更新：

```text
知识库/index.md
知识库/log.md
```

### 第 11 步：人工审核边界

请提醒用户：

```text
NotebookLM 生成的是课程素材，不是最终课程。
请你重点审核：
1. 事实是否准确
2. 案例是否适合你的受众
3. 讲义是否有你的观点
4. 哪些内容可以进入正式课程
```

Claude Code 不能替用户判断商业定位和最终观点，只能先整理素材、提出建议。

### 第 12 步：最终汇报

完成后，用简体中文汇报：

```text
课程主题：
NotebookLM notebook：
本地产物目录：
Obsidian 回写页面：
已生成产物：
失败或等待中的产物：
下一步建议：
```

---

## 常见问题

| 问题 | 处理 |
|---|---|
| NotebookLM 登录失效 | 执行 `nlm login` |
| 代理环境报 socksio | `uv tool install notebooklm-mcp-cli --with socksio --force` |
| studio 一直 in_progress | 等待 5-15 分钟，先下载已完成产物 |
| 下载命令失败 | 用 `nlm download xxx --help` 查看当前版本参数 |
| 内容质量一般 | 增加更好的 source，或者用 Claude Code 二次整理 |

