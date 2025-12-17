---
sidebar_label: Human Relay
description: 在 Roo Code 中使用 ChatGPT、Claude 或其他基于网页的 AI 模型，无需 API 密钥。手动在 Roo Code 和网页界面之间传递消息。
keywords:
  - human relay
  - roo code
  - 无需 api 密钥
  - chatgpt 网页版
  - claude 网页版
  - 手动中继
  - 网页 ai 模型
  - 免费 ai 访问
image: /img/social-share.jpg
---

# Human Relay 提供商

Human Relay 提供商允许你在 Roo Code 中使用基于网页的 AI 模型（如 ChatGPT 或 Claude），而无需 API 密钥。它依赖你手动在 Roo Code 和 AI 的网页界面之间传递消息。

---

## 工作原理

1.  **选择 Human Relay**：在 Roo Code 的设置中选择“Human Relay”作为你的 API 提供商。无需 API 密钥。
2.  **发起请求**：像往常一样在 Roo Code 中开始聊天或任务。
3.  **弹出对话框**：VS Code 中会弹出一个对话框。你发送给 AI 的消息会自动复制到剪贴板。
4.  **粘贴到网页 AI**：打开你选择的 AI 网页界面（例如 chat.openai.com、claude.ai），将剪贴板中的消息粘贴到聊天输入框。
5.  **复制 AI 回复**：AI 回复后，复制其完整的回复文本。
6.  **粘贴回 Roo Code**：回到 VS Code 的对话框，将 AI 的回复粘贴到指定字段，然后点击“确认”。
7.  **继续**：Roo Code 会将该回复作为直接来自 API 的响应进行处理。

---

## 使用场景

如果你符合以下情况，此提供商会很有用：

*   你想使用不提供直接 API 访问的模型。
*   你不想管理 API 密钥。
*   你需要利用仅在某些 AI 网页界面中可用的特定功能或上下文。

---

## 限制

*   **手动操作**：需要在 VS Code 和浏览器之间持续复制粘贴。
*   **交互较慢**：这种来回过程比直接 API 集成慢得多。
*   **出错风险**：手动复制粘贴可能引入错误或遗漏。

当你使用特定网页 AI 的好处超过手动中继的不便时，选择此提供商。