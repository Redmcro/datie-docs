# Claude Code 配置指南

## 第一步：安装 Claude Code

官网：[claude.ai/download](https://claude.ai/download)

**Windows / macOS：**

```bash
npm install -g @anthropic-ai/claude-code
```

## 第二步：配置 settings.json（推荐）

### 配置文件位置

| 系统 | 配置文件路径 |
|------|------------|
| Windows | `C:\Users\<用户名>\.claude\settings.json` |
| macOS | `~/.claude/settings.json` |

> 💡 没有 `.claude` 目录就手动创建一下

创建或编辑 `settings.json`，内容如下：

```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "替换为你的API Key",
    "ANTHROPIC_BASE_URL": "https://ai.datie.lol",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": 1
  },
  "permissions": {
    "allow": [],
    "deny": []
  }
}
```

### VSCode 插件用户

额外创建 `~/.claude/config.json`：

```json
{
  "primaryApiKey": "替换为你的API Key"
}
```

## 第三步：环境变量方式（可选）

> 💡 如果已经配了 `settings.json`，可以跳过这步

**Windows（PowerShell 管理员，永久生效）：**

```powershell
[System.Environment]::SetEnvironmentVariable('ANTHROPIC_BASE_URL', 'https://ai.datie.lol', 'User')
[System.Environment]::SetEnvironmentVariable('ANTHROPIC_AUTH_TOKEN', '替换为你的API Key', 'User')
```

**macOS（永久生效）：**

```bash
echo 'export ANTHROPIC_BASE_URL="https://ai.datie.lol"' >> ~/.zshrc
echo 'export ANTHROPIC_AUTH_TOKEN="替换为你的API Key"' >> ~/.zshrc
source ~/.zshrc
```

## 第四步：启动 Claude Code

```bash
cd 你的项目目录
claude
```

---

<a class="qq-btn" href="https://qm.qq.com/q/1051147956" target="_blank">遇到问题？加入QQ群</a>