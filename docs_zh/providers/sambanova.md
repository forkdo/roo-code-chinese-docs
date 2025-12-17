---
sidebar_label: SambaNova
description: 在 Roo Code 中配置 SambaNova 的高速 AI 模型。体验企业级推理性能，支持多种模型选择。
keywords:
  - sambanova
  - sambanova ai
  - roo code
  - api provider
  - high-speed inference
  - enterprise ai
  - llm provider
  - fast inference
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 SambaNova

SambaNova 专注于通过其可重构数据流单元（RDUs）和 SambaCloud 平台，为大语言模型提供高速推理服务。这为支持的模型带来了快速响应时间。

**官网：** [https://cloud.sambanova.ai/](https://cloud.sambanova.ai/)

---

## 获取 API 密钥

要在 Roo Code 中使用 SambaNova，你需要从 [SambaCloud](https://cloud.sambanova.ai?utm_source=roocode&utm_medium=external&utm_campaign=cloud_signup) 获取 API 密钥。注册后，在左侧面板中导航至 API 密钥部分，创建并复制你的 SambaCloud API 密钥。

---

## 可用模型

Roo Code 会自动从 SambaNova API 获取所有可用模型。

如需完整的、最新的模型列表和功能说明，请参阅 [SambaCloud 支持的模型文档](https://docs.sambanova.ai/cloud/docs/get-started/supported-models)。

---

## 在 Roo Code 中的配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标（<Codicon name="gear" />）。
2. **选择提供商：** 在“API Provider”下拉菜单中选择“SambaNova”。
3. **输入 API 密钥：** 将你的 SambaNova API 密钥粘贴到“SambaNova API Key”字段中。
4. **选择模型：** 从“Model”下拉菜单中选择你想要使用的模型。
5. **（可选）自定义基础 URL：** 如果使用私有部署，请勾选“Use custom base URL”并输入你的端点 URL。