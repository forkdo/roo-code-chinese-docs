---
sidebar_label: Glama
description: 通过 Glama 的统一 API 在 Roo Code 中访问多种 AI 模型。使用 Claude、OpenAI 和其他模型，并支持提示缓存和成本跟踪。
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
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Glama

Glama 通过统一的 API 提供对多种语言模型的访问，包括来自 Anthropic、OpenAI 等的模型。它提供提示缓存和成本跟踪等功能。

**官网：** [https://glama.ai/](https://glama.ai/)

---

## 获取 API 密钥

1.  **注册/登录：** 访问 [Glama 注册页面](https://glama.ai/sign-up)，使用 Google 账户或用户名/邮箱/密码注册。
2.  **获取 API 密钥：** 注册后，进入 [API 密钥页面](https://glama.ai/settings/gateway/api-keys) 获取 API 密钥。
3.  **复制密钥：** 复制显示的 API 密钥。

---

## 可用模型

Roo Code 会自动从 Glama 的统一 API 获取所有可用模型。

如需查看完整且最新的模型列表，请访问 [Glama 的模型页面](https://glama.ai/models)。

---

## 在 Roo Code 中的配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 在“API Provider”下拉菜单中选择“Glama”。
3.  **输入 API 密钥：** 将你的 Glama API 密钥粘贴到“Glama API Key”字段中。
4.  **选择模型：** 从“Model”下拉菜单中选择你想要使用的模型。

---

## 提示和注意事项

* **定价：** Glama 采用按使用量付费的模式。价格根据所选模型的不同而有所差异。