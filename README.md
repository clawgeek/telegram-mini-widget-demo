# Telegram 原生小组件最小 Demo（Bot API 10.4）

基于深潮 TechFlow 报道《Telegram 任意消息可变身应用，机器人可读取 TON 钱包余额》（2026.11.10）整理出的**最小可运行 demo**。

## 文章核心要点
- Telegram 创始人 Pavel Durov 宣布：**任意消息都可变成一个应用**。
- **Bot API 10.4** 新能力：机器人和 AI 智能体可在消息气泡内发送**原生 HTML 小组件**，支持动态布局、交互元素、原地更新，同一界面可在多条消息间复用。
- 体积 **<4KB**、即时加载、原生渲染。
- **TON 钱包集成**：小组件可读取用户钱包卡片（余额 + NFT 贴纸）、签名交易、识别转账服务消息；按钮点击可触发**仅点击者可见的临时回复**。
- Premium 用户最多可为两个机器人设置以 `agent` / `ai` / `app` / `game` 结尾的副用户名。

## 本 Demo 演示什么
一个 **TON 钱包卡片**原生小组件，覆盖文章提到的四项新能力：
1. 原生 HTML 渲染（黑底卡片，Telegram 风格）
2. 即时加载、<4KB（本例 **1358 字节**，富余约 67%）
3. 原地更新（点击「连接并签名」→ 余额 / NFT 原地刷新）
4. 仅点击者可见的临时回复（「交易已签名 ✓」）

## 文件说明
| 文件 | 作用 |
| --- | --- |
| `widget.html` | 核心：可直接嵌入 Bot API 的原生 HTML 小组件（1358 字节，<4KB） |
| `index.html` | 预览页：Telegram 风格气泡内嵌真实组件 + 源码展示 + 接入说明 |
| `bot-payload.json` | Bot API 10.4 `sendMessage` 调用示意（含组件 HTML 内联） |

## 本地运行
直接用浏览器打开 `index.html` 即可看到实时交互预览：

```bash
open index.html        # macOS
# 或起一个静态服务
python3 -m http.server 8080   # 然后访问 http://localhost:8080
```

## 接入真实机器人（Bot API 10.4）
1. BotFather 创建/升级机器人，确认 Bot API ≥ 10.4。
2. 调用 `sendMessage`，将 `widget.html` 的内容作为原生小组件字段下发（示意见 `bot-payload.json`）。
3. 需要真实钱包数据时，在 `onclick` 中接入 **TON Connect**，此时 `window.Telegram.WebApp` 已 `ready()`。
4. 「仅你可见」临时回复由 Telegram 端原生处理，无需自建后端。

> 注：Bot API 10.4 的原生组件字段名与完整协议以 [Telegram 官方文档](https://core.telegram.org/bots/api) 为准；本仓库以结构示意 + 可交互 UI 呈现核心能力，钱包数据为模拟值，仅作技术演示。

## 许可
MIT —— 可自由用于学习与二次开发。
