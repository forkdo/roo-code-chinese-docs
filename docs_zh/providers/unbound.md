---
description: 在 Roo Code 中配置 Unbound，通过单一 API 安全访问多个 LLM。企业级安全和合规功能。
keywords:
  - Unbound
  - Roo Code
  - LLM gateway
  - enterprise AI
  - secure AI
  - API provider
  - Anthropic
  - OpenAI
  - compliance
sidebar_label: Unbound
---

# 在 Roo Code 中使用 Unbound

Roo Code 支持通过 [Unbound](https://getunbound.ai/) 访问模型，这是一个专注于为各种大型语言模型 (LLM) 提供安全可靠访问的平台。Unbound 充当网关，允许您使用来自 Anthropic 和 OpenAI 等提供商的模型，而无需直接管理多个 API 密钥和配置。他们强调企业级使用的安全和合规功能。

**网站：** [https://getunbound.ai/](https://getunbound.ai/)

---

## 创建账户

1.  **注册/登录：** 访问 [Unbound 网关](https://gateway.getunbound.ai)。创建一个账户或登录。
2.  **创建应用程序：** 访问 [应用程序](https://gateway.getunbound.ai/ai-gateway-applications) 页面，然后点击“创建应用程序”按钮。
3.  **复制 API 密钥：** 将 API 密钥复制到剪贴板。

---

## 可用模型

Roo Code 会自动获取在您的 Unbound 应用程序中配置的所有模型。

在 [Unbound 应用程序仪表板](https://gateway.getunbound.ai/ai-gateway-applications) 中配置您允许的模型，然后 Roo Code 将在模型下拉菜单中显示它们。

---

## 在 Roo Code 中的配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“Unbound”。
3.  **输入 API 密钥：** 将您的 Unbound API 密钥粘贴到“Unbound API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择您所需的模型。

---

## 提示和注意事项

* **安全重点：** Unbound 强调企业级使用的安全功能。如果您的组织对 AI 使用有严格的安全要求，Unbound 可能是一个不错的选择。
*   **模型列表刷新：** Roo Code 在设置中专门为 Unbound 提供商包含了一个刷新按钮。这允许您轻松地从您的 Unbound 应用程序更新可用模型列表，并立即获得有关您的 API 密钥有效性的反馈。