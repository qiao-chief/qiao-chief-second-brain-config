# 乔帮主第二大脑配置包

这是一套给 Claude Code 读取和执行的 AI 第二大脑配置包。

它的目标不是教你多学一个工具，而是让 Claude Code 真正进入你的资料现场：会读取你的网页剪藏，会整理你的知识库，会把 NotebookLM、GitHub Pages、课程网页和产物记录回写到 Obsidian。

## 乔帮主欢迎语

你好，我是乔帮主。

这份配置包，是给有经验的人准备的第一块 AI 工作台地基。

你不用先成为程序员，也不用把所有工具都学明白。你只需要把这份文件交给 Claude Code，让它按步骤帮你安装、连接、验证。等这套第二大脑跑起来，你的网页剪藏、课程资料、外网素材、创作产物，就不再是一堆散乱文件，而会慢慢变成 AI 能读懂、能调用、能复用的经验资产。

先别急着追工具。我们先让 AI 认识你。

## 在线演示

https://qiao-chief.github.io/qiao-chief-second-brain-config/

## 配置包总链路

```text
00 从这里开始（本文件）
    ↓
01 连接 GitHub
    ↓
02 连接 Obsidian 第二大脑
    ↓
03 连接 NotebookLM 课程素材工厂
    ↓
04 生成教学驾驶舱
    ↓
回写 Obsidian，沉淀执行记录
```

## 当前正式版包含

| 部分 | 说明 | 状态 |
|---|---|---|
| **GitHub 能力包** | Agent 可读取和执行的配置文档 | 已完成 |
| **Obsidian 演示库** | 展示用户最终可以得到的第二大脑形态 | 已完成 |
| **NotebookLM 课程素材** | 讲义、测验、信息图、授课PPT | 全部已完成 |
| **教学驾驶舱** | 展示项目成果和入口链接的 HTML 页面 | 已完成 |

推荐对 Claude Code 说：

```text
请读取这个第二大脑配置包，并按里面的步骤帮我建立 Claude Code 第二大脑：
https://github.com/qiao-chief/qiao-chief-second-brain-config/blob/main/00-%E4%BB%8E%E8%BF%99%E9%87%8C%E5%BC%80%E5%A7%8B.md
```

第二步可以对 Claude Code 说：

```text
请读取这个 NotebookLM 课程素材工厂配置包，并按里面的步骤把我的课程资料生成PPT、信息图、讲义和测验：
https://github.com/qiao-chief/qiao-chief-second-brain-config/blob/main/03-%E8%BF%9E%E6%8E%A5NotebookLM%E8%AF%BE%E7%A8%8B%E7%B4%A0%E6%9D%90%E5%B7%A5%E5%8E%82.md
```

---

## 正式版 1.0 验证记录

2026-05-26，乔帮主第二大脑配置包已在全新的中文独立项目路径下完成完整链路测试，包含：

- **GitHub 能力包**：已 clone、整理根目录引导文档（00-04 + 常见问题）、更新 README
- **Obsidian 演示库**：已创建目录结构、首页、案例展示、执行记录，obsidian-secondbrain MCP 已指向新路径
- **NotebookLM 课程素材**：已生成课程讲义、测验题、信息图（PNG + JPG）、授课PPT（PDF + PPTX）
- **教学驾驶舱**：已生成最小可用 HTML 页面

执行记录见：`第二大脑配置包/执行记录/2026-05-26-乔帮主正式版1.0完整链路测试.md`
