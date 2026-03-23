# Codex 配置指南

## 第一步：找到配置文件

| 系统 | 配置文件路径 |
|------|------------|
| Windows | `C:\Users\<用户名>\.codex\config.toml` |
| macOS / Linux | `~/.codex/config.toml` |

> 💡 没有 `config.toml` 就先启动一次 Codex，它会自动创建

## 第二步：先备份（强烈建议）

> ⚠️ 先备份再改，改错了可以 1 秒回滚

**Windows（PowerShell）：**

```powershell
Copy-Item "$HOME\.codex\config.toml" "$HOME\.codex\config.toml.official"
```

**macOS / Linux：**

```bash
cp ~/.codex/config.toml ~/.codex/config.toml.official
```

## 第三步：设置环境变量（存放你的 Key）

> ⚠️ Codex 不支持在配置文件中直接填写明文 Key，必须通过环境变量传入。

**Windows（PowerShell）：**

```powershell
# 临时（仅当前终端有效）
$env:DATIE_API_KEY = "你的key"

# 永久（写入用户环境变量，重启终端后也生效）
[System.Environment]::SetEnvironmentVariable("DATIE_API_KEY", "你的key", "User")
```

**macOS / Linux：**

```bash
# 临时（仅当前终端有效）
export DATIE_API_KEY="你的key"

# 永久（写入 shell 配置文件）
echo 'export DATIE_API_KEY="你的key"' >> ~/.bashrc   # bash 用户
echo 'export DATIE_API_KEY="你的key"' >> ~/.zshrc    # zsh 用户
source ~/.bashrc  # 或 source ~/.zshrc
```

## 第四步：添加第三方 Provider

编辑 `config.toml`，示例：

```toml
model = "claude-opus-4-6-thinking"
model_provider = "datie"
personality = "pragmatic"

[features]
multi_agent = true

[model_providers.datie]
name = "Datie Proxy"
base_url = "https://ai.datie.lol/v1"
wire_api = "responses"
env_key = "DATIE_API_KEY"
```

> ⚠️ `env_key` 填的是**环境变量的名称**（如 `DATIE_API_KEY`），不是 Key 本身。Codex 启动时会自动读取该环境变量的值。

## 第五步：自定义模型（重点）

你只要改 `model = "..."` 就能切换默认模型。

> ⚠️ effort 在中转站都被覆盖了最高 无需自行添加了

## 第六步：建议做双配置（可选）

你可以保留两份配置，方便随时切换：

**保存当前第三方配置：**

```bash
cp ~/.codex/config.toml ~/.codex/config.toml.datie
```

**切回官方配置：**

```bash
cp ~/.codex/config.toml.official ~/.codex/config.toml
```

## 常见问题

**Q：报 401 / unauthorized？**  
→ Key 错了、过期了，或者环境变量没设置。检查方法：

```powershell
# Windows PowerShell
echo $env:DATIE_API_KEY
```

```bash
# macOS / Linux
echo $DATIE_API_KEY
```

如果输出为空，说明环境变量没生效，请回到第三步重新设置。

**Q：报 404 / model not found？**  
→ `base_url` 少了 `/v1`，或模型名拼错。

**Q：改了没生效？**  
→ 重启 Codex 应用后再试。

---

<a class="qq-btn" href="https://qm.qq.com/q/ThgG2Q7eMu" target="_blank">💬 遇到问题？加入QQ群</a>
