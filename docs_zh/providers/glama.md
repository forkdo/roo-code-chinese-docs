---
sidebar_label: Glama
description: 通过 Glama 的统一 API 在 Roo Code 中访问多个 AI 模型。使用 Claude、OpenAI 和其他模型，支持提示缓存和成本跟踪。
keywords:
  - glama
  - glama ai
  - roo code
  - api provider
  - unified api
  - claude models
  - openai models
  - prompt caching
  - cost tracking
---

# 在 Roo Code 中使用 Glama

Glama 通过统一 API 提供对各种语言模型的访问，包括来自 Anthropic、OpenAI 和其他厂商的模型。它提供提示缓存和成本跟踪等功能。

**网站：** [https://glama.ai/](https://glama.ai/)

---

## 获取 API 密钥

1.  **注册/登录：** 访问 [Glama 注册页面](https://glama.ai/sign-up)。使用 Google 账户或姓名/邮箱/密码进行注册。
2.  **获取 API 密钥：** 注册后，导航至 [API 密钥](https://glama.ai/settings/gateway/api-keys) 页面获取 API 密钥。
3.  **复制密钥：** 复制显示的 API 密钥。

---

## 可用模型

Roo Code 会自动从 Glama 的统一 API 获取所有可用模型。

有关完整且最新的模型列表，请参阅 [Glama 的模型页面](https://glama.ai/models)。

---

## 在 Roo Code 中的配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“Glama”。
3.  **输入 API 密钥：** 将您的 Glama API 密钥粘贴到“Glama API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择您所需的模型。

---

## 提示和注意事项

* **定价：** Glama 采用按使用量付费的模式。定价因您选择的模型而异。