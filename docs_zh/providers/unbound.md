---
description: 在 Roo Code 中配置 Unbound，通过单一 API 安全访问多种大语言模型。具备企业级安全和合规功能。
keywords:
  - Unbound
  - Roo Code
  - LLM 网关
  - 企业 AI
  - 安全 AI
  - API 提供商
  - Anthropic
  - OpenAI
  - 合规
image: /img/social-share.jpg
sidebar_label: Unbound
---

# 在 Roo Code 中使用 Unbound

Roo Code 支持通过 [Unbound](https://getunbound.ai/) 访问模型，该平台专注于提供对多种大语言模型（LLM）的安全可靠访问。Unbound 充当网关，允许您使用 Anthropic 和 OpenAI 等提供商的模型，而无需直接管理多个 API 密钥和配置。他们强调企业级的安全和合规功能。

**官网：** [https://getunbound.ai/](https://getunbound.ai/)

---

## 创建账户

1.  **注册/登录：** 访问 [Unbound 网关](https://gateway.getunbound.ai)，创建账户或登录。
2.  **创建应用：** 进入 [Applications 页面](https://gateway.getunbound.ai/ai-gateway-applications)，点击“Create Application”按钮。
3.  **复制 API 密钥：** 将 API 密钥复制到剪贴板。

---

## 可用模型

Roo Code 会自动获取您 Unbound 应用中配置的所有模型。

在 [Unbound Applications 仪表板](https://gateway.getunbound.ai/ai-gateway-applications) 中配置允许的模型后，Roo Code 将在模型下拉菜单中显示这些模型。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标（<Codicon name="gear" />）。
2.  **选择提供商：** 在“API Provider”下拉菜单中选择“Unbound”。
3.  **输入 API 密钥：** 将您的 Unbound API 密钥粘贴到“Unbound API Key”字段中。
4.  **选择模型：** 从“Model”下拉菜单中选择所需的模型。

---

## 提示和注意事项

* **安全重点：** Unbound 强调企业 AI 使用的安全功能。如果您的组织对 AI 使用有严格的安全要求，Unbound 可能是一个不错的选择。
*   **模型列表刷新：** Roo Code 在设置中为 Unbound 提供商专门添加了一个刷新按钮。这允许您轻松地从 Unbound 应用更新可用模型列表，并立即验证 API 密钥的有效性。