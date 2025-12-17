---
title: Baseten
sidebar_label: Baseten
description: 了解如何在 Roo Code 中配置和使用 Baseten 的模型 API。访问具有企业级性能、可靠性和竞争力价格的前沿开源模型。
keywords:
  - Baseten
  - 模型 API
  - 开源模型
  - DeepSeek
  - Kimi K2
  - Qwen
  - Roo Code
  - AI 集成
  - API 密钥
  - 企业推理
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Baseten

Baseten 提供按需的前沿模型 API，专为生产级应用设计，而不仅仅是实验用途。这些 API 基于 Baseten 推理栈构建，为来自 OpenAI、DeepSeek、Moonshot AI 和阿里巴巴云的领先开源模型提供优化的推理能力。

**官网：** [https://www.baseten.co/products/model-apis/](https://www.baseten.co/products/model-apis/)

---

## 获取 API 密钥

1. **注册/登录：** 访问 [Baseten](https://www.baseten.co/) 创建账户或登录。

2. **导航到 API 密钥：** 进入仪表盘，前往 API 密钥页面 [https://app.baseten.co/settings/api_keys](https://app.baseten.co/settings/api_keys)。

3. **创建密钥：** 生成一个新的 API 密钥。为其设置一个描述性名称（例如 "Roo Code"）。

4. **复制密钥：** 立即复制 API 密钥并安全保存。

---

## 可用模型

Roo Code 支持 Baseten 模型 API 提供的所有模型。

完整的最新模型列表和定价信息，请访问 [Baseten 的模型 API 页面](https://www.baseten.co/products/model-apis/)。

---

## 在 Roo Code 中的配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。

2. **选择提供商：** 在 "API Provider" 下拉菜单中选择 "Baseten"。

3. **输入 API 密钥：** 将你的 Baseten API 密钥粘贴到 "Baseten API Key" 字段中。

4. **选择模型：** 从 "Model" 下拉菜单中选择你想要的模型。

:::warning Kimi K2 思维模型
要使用 `moonshotai/Kimi-K2-Thinking` 模型，你必须在 Roo Code 设置中启用原生工具调用。此设置允许 Roo Code 通过模型的原生工具处理器调用工具，是此推理模型正常工作的必要条件。
:::

---

## 提示和注意事项

- **定价：** 请访问 [Baseten 模型 API 页面](https://www.baseten.co/products/model-apis/) 查看当前定价信息。