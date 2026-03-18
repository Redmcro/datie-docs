# OpenClaw 配置指南

OpenClaw 官网：[openclaw.ai](https://openclaw.ai)

## 第一步：修改配置文件

### 配置文件位置

| 系统 | 配置文件路径 |
|------|------------|
| Windows | `C:\Users\<用户名>\.openclaw\openclaw.json` |
| macOS | `~/.openclaw/openclaw.json` |

在 `openclaw.json` 的 `models.providers` 里新增一个 provider：

```json
"datie": {
  "baseUrl": "https://ai.datie.lol/v1",
  "apiKey": "你自己创建的密钥~",
  "api": "openai-completions",
  "models": [
    { "id": "gemini-3.1-pro-high", "name": "Gemini 3.1 Pro High" },
    { "id": "gemini-3-flash", "name": "Gemini 3 Flash" },
    { "id": "gemini-3.1-flash-image", "name": "Gemini 3.1 Flash Image", "input": ["text", "image"] }
  ]
}
```

> ⚠️ 改完后需重启 gateway：`openclaw gateway restart`

> 💡 provider 名字不一定叫 `datie`，随意命名，跟模型引用前缀一致就行

## 第二步：切换模型

聊天中直接发送命令即可切换，**不需要重启**，当场生效（仅当前 session 有效）：

| 命令 | 说明 |
|------|------|
| `/model datie/gemini-3.1-pro-high` | 切到思考模型 |
| `/model datie/gemini-3-flash` | 切到快速模型 |
| `model=default` | 恢复默认 |

## 第三步：设为默认模型（可选）

要**永久**修改默认模型，需要改配置 + 重启：

- **默认模型**：把 `agents.defaults.model.primary` 改成 `"datie/gemini-3.1-pro-high"`
- **画图/识图**：把 `agents.defaults.imageModel` 改成 `"datie/gemini-3.1-flash-image"`

```bash
openclaw gateway restart
```

---

<a class="qq-btn" href="https://qm.qq.com/q/ThgG2Q7eMu" target="_blank">💬 遇到问题？加入QQ群</a>