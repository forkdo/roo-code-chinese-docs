---
sidebar_label: DeepInfra
description: 在 Roo Code 中配置 DeepInfra 的高性能 AI 模型。通过提示缓存和视觉功能访问 Qwen Coder、Llama 和其他开源模型。
keywords:
  - deepinfra
  - deep infra
  - roo code
  - api provider
  - qwen coder
  - llama models
  - prompt caching
  - vision models
  - open source ai
---

# 在 Roo Code 中使用 DeepInfra

DeepInfra 提供对高性能开源模型的经济高效访问，具有提示缓存、视觉支持和专用编码模型等功能。其基础设施提供低延迟和跨全球边缘位置的自动负载均衡。

**网站：** [https://deepinfra.com/](https://deepinfra.com/)

---

## 获取 API 密钥

1. **注册/登录：** 访问 [DeepInfra](https://deepinfra.com/)。创建账户或登录。
2. **导航到 API 密钥：** 在仪表板中访问 API 密钥部分。
3. **创建密钥：** 生成一个新的 API 密钥。为其指定一个描述性名称（例如 "Roo Code"）。
4. **复制密钥：** **重要：** 立即复制 API 密钥。安全存储。

---

## 可用模型

Roo Code 会自动从 DeepInfra 的 API 获取所有可用模型。

有关完整、最新的模型目录，请参阅 [DeepInfra 的模型页面](https://deepinfra.com/models)。

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 从 "API 提供商" 下拉菜单中选择 "DeepInfra"。
3. **输入 API 密钥：** 将您的 DeepInfra API 密钥粘贴到 "DeepInfra API 密钥" 字段中。
4. **选择模型：** 从 "模型" 下拉菜单中选择您所需的模型。