---
description: 在 Roo Code 中配置 OpenRouter，通过单一 API 访问来自各种提供商的 100+ 种语言模型，支持自动模型发现。
keywords:
  - roo code
  - openrouter
  - ai provider
  - language models
  - api configuration
  - model selection
  - prompt caching
  - byok
sidebar_label: OpenRouter
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 OpenRouter

OpenRouter 是一个 AI 平台，通过单一 API 提供来自不同提供商的多种语言模型。这可以简化设置，并让您轻松尝试不同的模型。

**官网：** [https://openrouter.ai/](https://openrouter.ai/)

---

## 获取 API 密钥

1.  **注册/登录：** 访问 [OpenRouter 官网](https://openrouter.ai/)，使用 Google 或 GitHub 账号登录。
2.  **获取 API 密钥：** 进入 [密钥页面](https://openrouter.ai/keys)，您应该能看到已列出的 API 密钥。如果没有，请创建一个新密钥。
3.  **复制密钥：** 复制您的 API 密钥。

---

## 可用模型

Roo Code 会自动从 OpenRouter API 获取所有可用模型（来自多个提供商的 100+ 模型）。

如需完整的、最新的模型列表及定价和功能详情，请访问 [OpenRouter 的模型页面](https://openrouter.ai/models)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标（<Codicon name="gear" />）。
2.  **选择提供商：** 在“API Provider”下拉菜单中选择“OpenRouter”。
3.  **输入 API 密钥：** 将您的 OpenRouter API 密钥粘贴到“OpenRouter API Key”字段中。
4.  **选择模型：** 从“Model”下拉菜单中选择您想要的模型。
5.  **（可选）自定义基础 URL：** 如果需要使用自定义的 OpenRouter API 基础 URL，请勾选“Use custom base URL”并输入 URL。大多数用户保持默认（留空）即可。

---

## 支持的消息转换

OpenRouter 提供了一种 [可选的“中间层”消息转换](https://openrouter.ai/docs/features/message-transforms)，帮助处理超出模型最大上下文大小的提示。您可以通过勾选“Compress prompts and message chains to the context size”框来启用。

---

## 提示与注意事项

* **模型选择：** OpenRouter 提供多种模型。请尝试找到最适合您需求的模型。
* **定价：** OpenRouter 按底层模型的定价收费。详情请见 [OpenRouter 模型页面](https://openrouter.ai/models)。
*   **提示缓存：**
    *   OpenRouter 会将缓存请求传递给支持该功能的底层模型。请查看 [OpenRouter 模型页面](https://openrouter.ai/models) 了解哪些模型提供缓存。
    *   对于大多数模型，如果模型本身支持缓存，缓存会自动激活（类似于 Requesty 的工作方式）。
    *   **支持提示缓存的模型包括：**
        *   Anthropic Claude Sonnet 3.5、3.7
        *   Anthropic Claude Haiku 3.5
        *   **Anthropic Claude Haiku 4.5**（新增）
        *   Google Gemini 模型（需手动激活 - 见下文）
    *   **通过 OpenRouter 使用 Gemini 模型的例外情况：** 由于通过 OpenRouter 访问 Google 的缓存机制时，有时会遇到响应延迟，因此*专门针对 Gemini 模型*需要手动激活步骤。
    *   如果您通过 OpenRouter 使用 **Gemini 模型**，则**必须**在提供商设置中手动勾选“Enable Prompt Caching”框以激活该模型的缓存。此复选框作为临时解决方案。对于 OpenRouter 上的非 Gemini 模型，此复选框对缓存并非必需。
*   **自带密钥（BYOK）：** 如果您使用自己的密钥连接底层服务，OpenRouter 将收取正常费用的 5%。Roo Code 会自动调整成本计算以反映这一点。