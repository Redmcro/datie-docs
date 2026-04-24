# Codex 配置指南

> Codex 仅支持 OpenAI 协议，不要填写 `claude-*` 模型名。  
> Codex App / Codex CLI 通用。

## 1. 配置文件位置

| 系统 | `auth.json` | `config.toml` |
|------|-------------|---------------|
| Windows | `C:\Users\<用户名>\.codex\auth.json` | `C:\Users\<用户名>\.codex\config.toml` |
| macOS / Linux | `~/.codex/auth.json` | `~/.codex/config.toml` |

> 如果没有这些文件或目录，就自己创建。

## 2. 写入 API Key（`auth.json`）

打开 `auth.json`，写入下面内容：

```json
{
  "OPENAI_API_KEY": "这里填写你的key~"
}
```

## 3. 写入主配置（`config.toml`）

打开 `config.toml`，写入下面内容：

```toml
model_provider = "OpenAI"
model = "gpt-5.5"
review_model = "gpt-5.5"
model_reasoning_effort = "xhigh"
disable_response_storage = true
network_access = "enabled"
windows_wsl_setup_acknowledged = true
model_context_window = 1000000
model_auto_compact_token_limit = 900000

[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://ai.datie.lol/v1"
wire_api = "responses"
requires_openai_auth = true
```

## 4. 重启 Codex

保存两个文件后，重启 Codex 即可生效。
