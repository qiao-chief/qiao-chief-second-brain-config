# 01：连接 GitHub

> 用途：让 Claude Code 检查 Git 和 GitHub CLI 环境，完成登录验证，并确认能创建仓库和发布 GitHub Pages。

---

## 给 Claude Code 的执行说明

请按顺序执行，不要跳步。

### 第 0 步：说明执行原则

请先告诉用户：

```text
我会先检查环境，再补齐缺失工具。遇到需要浏览器登录或授权的地方，我会暂停等你操作。已有配置不会直接覆盖，会先确认。
```

### 第 1 步：检查 Claude Code

```bash
claude --version
which claude
```

如果 Claude Code 不存在：

1. 先检查 Node.js：

```bash
node --version
npm --version
```

2. 如果 Node.js 不存在，请按系统安装：

```bash
# macOS
brew install node

# Windows
winget install --id OpenJS.NodeJS --accept-source-agreements --accept-package-agreements
```

3. 安装 Claude Code：

```bash
npm install -g @anthropic-ai/claude-code
```

4. 验证：

```bash
claude --version
claude mcp list
```

### 第 2 步：检查 GitHub 环境

```bash
git --version
gh --version
gh auth status
```

如果 Git 不存在：

```bash
# macOS
xcode-select --install

# Windows
winget install --id Git.Git --accept-source-agreements --accept-package-agreements
```

如果 GitHub CLI 不存在：

```bash
# macOS
brew install gh

# Windows
winget install --id GitHub.cli --accept-source-agreements --accept-package-agreements
```

如果 `gh auth status` 显示未登录：

```bash
gh auth login --web --git-protocol https
```

请暂停，让用户在浏览器中完成 GitHub 授权。

登录后执行：

```bash
gh auth status
gh auth setup-git
```

`gh auth setup-git` 很重要，用来解决 `git push` 时读不到 GitHub 凭证的问题。

### 第 3 步：GitHub 调试验证

创建一个最小测试仓库，验证 Claude Code 能否 push：

```bash
mkdir -p "$HOME/Documents/claude-github-test"
cd "$HOME/Documents/claude-github-test"
cat > index.html <<'HTML'
<!doctype html>
<html lang="zh-CN">
<head><meta charset="utf-8"><title>Claude GitHub Test</title></head>
<body><h1>GitHub 连接成功</h1></body>
</html>
HTML

git init
git add index.html
git commit -m "初始化 GitHub 测试"
gh repo create claude-github-test --public --source=. --push
```

启用 GitHub Pages：

```bash
gh api repos/{owner}/claude-github-test/pages --method POST -F 'source[branch]=main' -F 'source[path]=/'
```

如果 `{owner}` 不能自动识别，先执行：

```bash
gh api user --jq .login
```

等待 30-90 秒后检查：

```bash
curl -I -L "https://{owner}.github.io/claude-github-test/"
```

必须看到 `HTTP/2 200`。

常见问题：

| 问题 | 处理 |
|---|---|
| `could not read Username for https://github.com` | 执行 `gh auth setup-git` 后重试 |
| Pages 第一次 404 | 等 1-2 分钟，再查 Action 状态 |
| API 提示 gh-pages branch 不存在 | 重新用 `source[branch]=main` 和 `source[path]=/` 启用 |

### 第 4 步：清理测试仓库（可选）

如果用户不需要保留测试仓库：

```bash
gh repo delete claude-github-test --yes
rm -rf "$HOME/Documents/claude-github-test"
```

---

## 下一步

GitHub 连接完成后，继续读取 `02-连接Obsidian第二大脑.md`。
