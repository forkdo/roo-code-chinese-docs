---
sidebar_label: Groq
description: 在 Roo Code 中配置 Groq 的高速 LPU 推理。以显著更快的响应时间访问 Llama、Mixtral 等模型。
keywords:
  - groq
  - groq cloud
  - roo code
  - api provider
  - lpu
  - fast inference
  - llama models
  - mixtral
  - high speed ai
---

# 使用 Groq 与 Roo Code

Groq 专注于利用其定制的 Language Processing Units（LPU）为大型语言模型提供极高速的推理能力，从而显著缩短支持模型的响应时间。

**官网：** [https://groq.com/](https://groq.com/)

---

## 获取 API 密钥

要在 Roo Code 中使用 Groq，您需要从 [GroqCloud 控制台](https://console.groq.com/) 获取一个 API 密钥。注册或登录后，进入仪表板中的 API 密钥部分，创建并复制您的密钥。

---

## 可用模型

Roo Code 会自动从 Groq API 获取所有可用模型。

有关完整且最新的模型列表及其功能，请参阅 [Groq 的模型文档](https://console.groq.com/docs/models)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API Provider”下拉菜单中选择 "Groq"。
3.  **输入 API 密钥：** 将您的 Groq API 密钥粘贴到“Groq API Key”字段中。
4.  **选择模型：** 从“Model”下拉菜单中选择您需要的模型。