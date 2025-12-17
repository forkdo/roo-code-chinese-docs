---
sidebar_label: Mistral AI
description: 配置 Roo Code 使用 Mistral AI 模型，包括用于代码生成的 Codestral，支持函数调用和视觉功能。
keywords:
  - Mistral AI
  - Codestral
  - Roo Code
  - AI 模型
  - 代码生成
  - Pixtral
  - Ministral
  - 函数调用
  - La Plateforme
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Mistral AI

Roo Code 支持通过 Mistral AI API 访问模型，包括标准 Mistral 模型和专门用于代码的 Codestral 模型。

**官网：** [https://mistral.ai/](https://mistral.ai/)

---

## 获取 API 密钥

1.  **注册/登录：** 访问 [Mistral 平台](https://console.mistral.ai/)。创建账户或登录。您可能需要完成验证流程。
2.  **创建 API 密钥：**  
    - [La Plateforme API 密钥](https://console.mistral.ai/api-keys/) 和/或 
    - [Codestral API 密钥](https://console.mistral.ai/codestral)

---

## 可用模型

Roo Code 支持 Mistral AI API 提供的所有模型。

如需完整的、最新的模型列表和功能说明，请参阅 [Mistral 的模型文档](https://docs.mistral.ai/getting-started/models/models_overview/)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API Provider”下拉菜单中选择“Mistral”。
3.  **输入 API 密钥：** 如果使用 `mistral` 模型，请将 Mistral API 密钥粘贴到“Mistral API Key”字段中。如果要使用 `codestral-latest`，请参阅下方的“Codestral”部分。
4.  **选择模型：** 从“Model”下拉菜单中选择您需要的模型。

---

## 使用 Codestral

[Codestral](https://docs.mistral.ai/capabilities/code_generation/) 是专为代码生成和交互设计的模型。 
仅对于 Codestral，您可以使用不同的端点（默认：codestral.mistral.ai）。 
对于 La Plateforme API 密钥，请将 **Codestral Base Url** 更改为：https://api.mistral.ai 

使用 Codestral 的步骤：

1.  **选择“Mistral”作为 API 提供商。**
2.  **选择一个 Codestral 模型**
3.  **输入您的 Codestral (codestral.mistral.ai) 或 La Plateforme (api.mistral.ai) API 密钥。**