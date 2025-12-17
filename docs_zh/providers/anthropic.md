---
sidebar_label: Anthropic
description: 在 Roo Code 中配置 Anthropic 的 Claude AI 模型。使用提示缓存和大上下文窗口访问 Claude Opus、Sonnet 和 Haiku 模型。
keywords:
  - anthropic
  - claude
  - claude ai
  - roo code
  - api provider
  - claude opus
  - claude sonnet
  - claude haiku
  - prompt caching
  - ai models
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Anthropic

Anthropic 是一家专注于 AI 安全和研究的公司，致力于构建可靠、可解释且可控的 AI 系统。他们的 Claude 模型以其强大的推理能力、乐于助人和诚实可靠而著称。

**官网：** [https://www.anthropic.com/](https://www.anthropic.com/)

---

## 获取 API 密钥

1.  **注册/登录：** 访问 [Anthropic 控制台](https://console.anthropic.com/)。注册账户或登录。
2.  **导航至 API 密钥：** 进入 [API 密钥](https://console.anthropic.com/settings/keys) 页面。
3.  **创建密钥：** 点击“创建密钥”。为密钥输入一个描述性名称（例如，“Roo Code”）。
4.  **复制密钥：** **重要：** 立即复制 API 密钥。此密钥仅显示一次，之后将无法再次查看。请安全保存。

---

## 可用模型

Roo Code 支持 Anthropic API 提供的所有 Claude 模型。

如需获取完整、最新的模型列表和功能说明，请参阅 [Anthropic 的模型文档](https://docs.anthropic.com/en/docs/about-claude/models)。

---

## 在 Roo Code 中的配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 在“API 提供商”下拉菜单中选择“Anthropic”。
3.  **输入 API 密钥：** 将你的 Anthropic API 密钥粘贴到“Anthropic API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择你想要的 Claude 模型。
5.  **（可选）自定义基础 URL：** 如果需要使用自定义的基础 URL 访问 Anthropic API，请勾选“使用自定义基础 URL”并输入 URL。大多数用户无需调整此项。

---

## 提示与注意事项

*   **提示缓存：** Claude 模型支持 [提示缓存](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching)，可显著降低重复提示的成本和延迟。
*   **上下文窗口：** Claude 模型具有较大的上下文窗口（200,000 tokens），允许在提示中包含大量代码和上下文信息。
*   **定价：** 请参考 [Anthropic 定价](https://www.anthropic.com/pricing) 页面获取最新价格信息。
*   **速率限制：** Anthropic 根据 [使用层级](https://docs.anthropic.com/en/api/rate-limits#requirements-to-advance-tier) 实施严格的速率限制。如果反复遇到速率限制，可考虑联系 Anthropic 销售部门，或通过 [OpenRouter](/providers/openrouter) 或 [Requesty](/providers/requesty) 等其他提供商访问 Claude。