# 乔帮主第二大脑配置包

这是一套给 Claude Code 读取和执行的 AI 第二大脑配置包。

它的目标不是教你多学一个工具，而是让 Claude Code 真正进入你的资料现场：会读取你的 Clippings，会整理你的知识库，会把 NotebookLM、GitHub Pages、课程网页和产物记录回写到 Obsidian。

## 乔帮主欢迎语

你好，我是乔帮主。

这份配置包，是给有经验的人准备的第一块 AI 工作台地基。

你不用先成为程序员，也不用把所有工具都学明白。你只需要把这份文件交给 Claude Code，让它按步骤帮你安装、连接、验证。等这套第二大脑跑起来，你的网页剪藏、课程资料、外网素材、创作产物，就不再是一堆散乱文件，而会慢慢变成 AI 能读懂、能调用、能复用的经验资产。

先别急着追工具。我们先让 AI 认识你。

## 在线演示

https://qiao-chief.github.io/qiao-chief-second-brain-config/

## 新账号测试记录

2026-05-26 已使用 NotebookLM 账号 `mellingerphjxe@gmail.com` 重新跑通课程素材工厂链路。

本次验证结果：

- NotebookLM 可通过 `qiao-es` profile 正常登录和切换
- 课程素材分析、授课简报、信息图、课程讲义、测验题均已生成
- 配置包 02 已补充多账号切换说明和当前 CLI 参数差异
- 执行记录见：`第二大脑配置包/执行记录/2026-05-26-新账号课程素材工厂测试.md`

## 配置包

**01 第二大脑配置包**

把下面这个文件链接交给 Claude Code，它会按说明检查环境、安装工具、创建测试 vault，并连接 Obsidian：

https://github.com/qiao-chief/qiao-chief-second-brain-config/blob/main/%E7%AC%AC%E4%BA%8C%E5%A4%A7%E8%84%91%E9%85%8D%E7%BD%AE%E5%8C%85/01-%E7%AC%AC%E4%BA%8C%E5%A4%A7%E8%84%91%E9%85%8D%E7%BD%AE%E5%8C%85.md

**02 NotebookLM 课程素材工厂配置包**

把课程资料交给 Claude Code，让它调用 NotebookLM 生成简报、信息图、讲义、测验，并回写到第二大脑：

https://github.com/qiao-chief/qiao-chief-second-brain-config/blob/main/%E7%AC%AC%E4%BA%8C%E5%A4%A7%E8%84%91%E9%85%8D%E7%BD%AE%E5%8C%85/02-NotebookLM%E8%AF%BE%E7%A8%8B%E7%B4%A0%E6%9D%90%E5%B7%A5%E5%8E%82%E9%85%8D%E7%BD%AE%E5%8C%85.md

推荐对 Claude Code 说：

```text
请读取这个第二大脑配置包，并按里面的步骤帮我建立 Claude Code 第二大脑：
https://github.com/qiao-chief/qiao-chief-second-brain-config/blob/main/%E7%AC%AC%E4%BA%8C%E5%A4%A7%E8%84%91%E9%85%8D%E7%BD%AE%E5%8C%85/01-%E7%AC%AC%E4%BA%8C%E5%A4%A7%E8%84%91%E9%85%8D%E7%BD%AE%E5%8C%85.md
```

第二步可以对 Claude Code 说：

```text
请读取这个 NotebookLM 课程素材工厂配置包，并按里面的步骤把我的课程资料生成简报、信息图、讲义和测验：
https://github.com/qiao-chief/qiao-chief-second-brain-config/blob/main/%E7%AC%AC%E4%BA%8C%E5%A4%A7%E8%84%91%E9%85%8D%E7%BD%AE%E5%8C%85/02-NotebookLM%E8%AF%BE%E7%A8%8B%E7%B4%A0%E6%9D%90%E5%B7%A5%E5%8E%82%E9%85%8D%E7%BD%AE%E5%8C%85.md
```

---

## 正式版 1.0 验证记录

2026-05-26，乔帮主第二大脑配置包已在全新的中文独立项目路径下完成完整链路测试，包含 GitHub 能力包、Obsidian 演示库、NotebookLM 课程素材和最小教学驾驶舱。
