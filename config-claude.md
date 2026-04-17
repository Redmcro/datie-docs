# Claude Code 配置指南

## 第一步：安装 Claude Code

官网：[claude.ai/download](https://claude.ai/download)

**Windows / macOS：**

```bash
npm install -g @anthropic-ai/claude-code
```

## 第二步：配置 settings.json

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
    "ANTHROPIC_BASE_URL": "https://ai.datie.lol",
    "ANTHROPIC_AUTH_TOKEN": "替换为你的API Key",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "CLAUDE_CODE_ATTRIBUTION_HEADER": "0"
  }
}
```

### VSCode 插件用户

在 VSCode 扩展市场搜索并安装 `Claude Code for VSCode`，配置同上。
