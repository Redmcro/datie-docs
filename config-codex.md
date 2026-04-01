# Codex 配置指南

> Codex 仅支持 OpenAI 协议，不要填写 `claude-*` 模型名。  
> Codex App / Codex Cli 通用此教程

## 1. 配置文件位置

| 系统 | `auth.json` | `config.toml` |
|------|-------------|---------------|
| Windows | `C:\Users\<用户名>\.codex\auth.json` | `C:\Users\<用户名>\.codex\config.toml` |
| macOS / Linux | `~/.codex/auth.json` | `~/.codex/config.toml` |

> 没有文件就先启动一次 Codex，会自动创建目录。

## 2. 写入 API Key（`auth.json`）

```json
{
  "OPENAI_API_KEY": "这里填写你的key~"
}
```

## 3. 写入主配置（`config.toml`）

```toml
model_provider = "OpenAI"
model = "gpt-5.4"
review_model = "gpt-5.4"
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

> ⚠️⚠️ **警告：模型只有以下两个，填写其他模型会直接报错或不可用。**
>
> - `gpt-5.4`
> - `gpt-5.3-codex`


## 4. 常见问题

**401（未授权）**

- `auth.json` 未生效、Key 无效或过期。
- 检查 `~/.codex/auth.json` 是否为合法 JSON，且键名必须是 `OPENAI_API_KEY`。

**404（模型不存在）**

- 模型名不在支持列表（只支持 `gpt-5.4`、`gpt-5.3-codex`）。
- `base_url` 配置错误 注意多了个/v1。

**修改后没生效**

- 重启 Codex 再试。

---

<a class="qq-btn" href="https://qm.qq.com/q/ThgG2Q7eMu" target="_blank">💬 遇到问题？加入QQ群</a>
