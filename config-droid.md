# Droid 安装配置指南

Droid 官网：[factory.ai/product/ide](https://factory.ai/product/ide)

## 第一步：安装 Droid

**Windows：**

```powershell
irm https://app.factory.ai/cli/windows | iex
```

**macOS：**

```bash
curl -fsSL https://app.factory.ai/cli | sh
```

## 第二步：设置环境变量（必须）

> ⚠️ 这里是为了绕过登录，配置个假的就行~

**Windows（PowerShell 管理员）：**

```powershell
[System.Environment]::SetEnvironmentVariable("FACTORY_API_KEY", "fk-your-key-here", "User")
```

**macOS：**

```bash
echo 'export FACTORY_API_KEY="fk-your-key-here"' >> ~/.zshrc
source ~/.zshrc
```

## 第三步：修改配置文件

### 配置文件位置

| 系统 | 配置文件路径 |
|------|------------|
| Windows | `C:\Users\<用户名>\.factory\config.json` |
| macOS | `~/.factory/config.json` |

> 💡 没有 `config.json` 就手动创建一下

> 💡 每次改完都记得删除 `settings.json`，没有的话无视这条~

### 添加配置

在 `config.json` 中添加以下内容：

```json
{
  "custom_models": [
    {
      "model_display_name": "Opus 4.6",
      "model": "claude-opus-4-6-thinking",
      "base_url": "https://ai.datie.lol",
      "api_key": "你自己创建的密钥~",
      "provider": "anthropic",
      "max_tokens": 8192
    }
  ]
}
```

## 第四步：启动 Droid

```bash
cd 你的项目目录
droid
```

### 常用命令

| 命令 | 说明 |
|------|------|
| `/model` | 切换模型 |
| `/setting` | 设置默认模型 |

---

<a class="qq-btn" href="https://qm.qq.com/q/1051147956" target="_blank">遇到问题？加入QQ群</a>
