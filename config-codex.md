# Codex 配置指南

> Codex 仅支持 OpenAI 协议，不要填写 `claude-*` 模型名。  
> Codex App / Codex CLI 通用。

## 1. 配置文件位置

| 系统 | `auth.json` | `config.toml` |
|------|-------------|---------------|
| Windows | `C:\Users\<用户名>\.codex\auth.json` | `C:\Users\<用户名>\.codex\config.toml` |
| macOS / Linux | `~/.codex/auth.json` | `~/.codex/config.toml` |

> 没有文件就先启动一次 Codex，会自动创建目录。

## 2. 先备份 `config.toml`（推荐）

> ⚠️ 推荐先备份为 `config.toml.bak`，后续切换和回滚更快。

**Windows（PowerShell）**

```powershell
Copy-Item "$HOME\.codex\config.toml" "$HOME\.codex\config.toml.bak" -Force
```

**macOS / Linux**

```bash
cp ~/.codex/config.toml ~/.codex/config.toml.bak
```

## 3. 写入 API Key（`auth.json`）

```json
{
  "OPENAI_API_KEY": "这里填写你的key~"
}
```

## 4. 写入主配置（`config.toml`）

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

## 5. 首次保存 `config.toml.datie`（可选）

首次配置完成后，保存当前配置：

**Windows（PowerShell）**

```powershell
Copy-Item "$HOME\.codex\config.toml" "$HOME\.codex\config.toml.datie" -Force
```

**macOS / Linux**

```bash
cp ~/.codex/config.toml ~/.codex/config.toml.datie
```

## 6. 一键切换 `config.toml`（可选）

完成上一步后，可直接一键切换：

**Windows（PowerShell）**

```powershell
# 切到 datie 配置
Copy-Item "$HOME\.codex\config.toml.datie" "$HOME\.codex\config.toml" -Force

# 切回官方/备份配置
Copy-Item "$HOME\.codex\config.toml.bak" "$HOME\.codex\config.toml" -Force
```

**macOS / Linux**

```bash
# 切到 datie 配置
cp ~/.codex/config.toml.datie ~/.codex/config.toml

# 切回官方/备份配置
cp ~/.codex/config.toml.bak ~/.codex/config.toml
```

## 7. 常见问题

**401（未授权）**

- 常见原因：`auth.json` 未生效、Key 无效或已过期。
- 检查 `~/.codex/auth.json` 是否是合法 JSON，且键名为 `OPENAI_API_KEY`。

**404（模型不存在）**

- 模型名不在支持列表（只支持 `gpt-5.4`、`gpt-5.3-codex`）。
- `base_url` 配置错误（常见是少了 `/v1`）。

**修改后没生效**

- 重启 Codex 再试。

**直接切换toml有影响吗？**

- `key` 登录：只切 `config.toml` 通常不影响； 不行的话可执行 `codex logout`重头来过。
- 账号登录：只切 `config.toml` 一般无影响。

