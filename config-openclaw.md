# OpenClaw 模型配置指南

> 适用版本：2026.3.x ｜ 官网：[openclaw.ai](https://openclaw.ai) ｜ 社区：[Discord](https://discord.com/invite/clawd)

---

## 一、让龙虾配置（复制发给他）

复制下面这段，直接发给你的小龙虾：

---

> 在 `~/.openclaw/openclaw.json` 的 `models.providers` 里新增一个 provider，命名为 `datie`：
>
> ```json
> "datie": {
>   "baseUrl": "https://ai.datie.lol/v1",
>   "apiKey": "你自己的密钥",
>   "api": "openai-completions",
>   "models": [
>     { "id": "gemini-3.1-pro-high", "name": "Gemini 3.1 Pro High" },
>     { "id": "gemini-3-flash", "name": "Gemini 3 Flash" },
>     { "id": "gemini-3.1-flash-image", "name": "Gemini 3.1 Flash Image", "input": ["text", "image"] }
>   ]
> }
> ```
>
> 改完运行 `openclaw gateway restart`。


> ⚠️ 不一定叫datie, 随意起一个就行🐱~
---

## 一b. 让龙虾学会画图（复制发给他）

> 内置的 `image` 工具只支持看图，**不支持生成图片**。画图要用 curl 直调 API，流程如下：
>
> **第 1 步：发请求**
>
> ```bash
> curl -s https://ai.datie.lol/v1/chat/completions \
>   -H "Content-Type: application/json" \
>   -H "Authorization: Bearer 你的密钥" \
>   -d '{
>     "model": "gemini-3.1-flash-image",
>     "messages": [{"role": "user", "content": "画一只猫"}]
>   }' > /tmp/image_response.json
> ```
>
> **第 2 步：用 Python 提取图片并保存**
>
> ```python
> import json, base64
>
> with open('/tmp/image_response.json') as f:
>     data = json.load(f)
>
> images = data['choices'][0]['message'].get('images', [])
> if images:
>     b64_data = images[0]['image_url']['url'].split('base64,')[1]
>     with open('output.png', 'wb') as f:
>         f.write(base64.b64decode(b64_data))
>     print("saved: output.png")
> else:
>     print("没有返回图片")
> ```
>
> **第 3 步：发送给用户** 用 `MEDIA:./output.png`
>
> ⚠️ 注意事项：
> - 图片在 `images` 数组里，**不在** `content` 字段（`content` 可能是 `null`）
> - **不要在 shell 变量里传 base64**，会截断/出错。用 Python 脚本一步到位
> - 中文 prompt 完全没问题
>
> 识图也可以用类似方式，把图片 base64 编码后放进 message 的 content 数组发送。

---

## 二、切换模型（你直接在聊天里说）

| 说这个 | 效果 |
|--------|------|
| `/model datie/gemini-3.1-pro-high` | 切到思考模型（复杂任务用） |
| `/model datie/gemini-3-flash` | 切到快速模型（日常用） |
| `/model default` | 恢复默认 |
| "换成思考模型" | 说人话也行，龙虾能懂 |

> 切换**不用重启**，当场生效。只在当前会话有效。

---

## 三、设为默认（可选）

让龙虾把 `agents.defaults` 改成：

- `model.primary` → `"datie/gemini-3.1-pro-high"`（默认聊天模型）
- `imageModel` → `"datie/gemini-3.1-flash-image"`（默认看图/画图模型）

改完重启。

---

## 四、三个模型分别是干嘛的

| 模型 | 用途 |
|------|------|
| **gemini-3.1-pro-high** | 深度思考，写长文、分析复杂问题 |
| **gemini-3-flash** | 快速问答，日常聊天，省 token |
| **gemini-3.1-flash-image** | 看图 + 画图（同一个模型） |

---

## 五、画图和识图

### 识图（让龙虾看图片）
直接在聊天里**发图片**给龙虾，他会自动分析。

### 画图（让龙虾生成图片）
直接说就行，比如：
- "帮我画一只猫"
- "画一个赛博朋克风格的城市夜景"
- "生成一张像素风格的头像"

> ⚠️ 画图需要龙虾配置好才能用。如果龙虾说不会画，让他照着上面的配置说明设置 `imageModel`。

---

## 六、常见问题

**Q：改了配置没生效？**
→ 没重启。跑 `openclaw gateway restart`

**Q：切了模型没变化？**
→ `/model` 只在当前会话生效，重开会话就恢复默认了。想永久生效要改配置。

**Q：怎么让龙虾画图？**
→ 直接说"帮我画一个xxx"就行。

**Q：怎么让龙虾看图？**
→ 直接发图片就行。

**Q：模型报 404？**
→ baseUrl 末尾要 `/v1`，模型 ID 拼写要对。