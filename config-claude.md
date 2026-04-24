# Claude Code 配置指南

## 1. 安装 Claude Code

官网：[claude.ai/download](https://claude.ai/download)

```bash
npm install -g @anthropic-ai/claude-code
```

## 2. 配置文件位置

| 系统 | 配置文件路径 |
|------|------------|
| Windows | `C:\Users\<用户名>\.claude\settings.json` |
| macOS | `~/.claude/settings.json` |

> 如果没有这些文件或目录，就自己创建。

## 3. 写入配置（`settings.json`）

打开 `settings.json`，写入下面内容：

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

## 4. 重启 Claude Code

保存文件后，重启 Claude Code 即可生效。

如果使用 VSCode 插件，在 VSCode 扩展市场搜索并安装 `Claude Code for VSCode`，配置同上。
