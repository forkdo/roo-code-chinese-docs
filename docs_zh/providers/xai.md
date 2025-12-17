---
description: 在 Roo Code 中配置 xAI 的 Grok 模型。访问 Grok-4、Grok-3、Grok-2 和视觉模型，支持大上下文窗口、推理能力和提示缓存。
keywords:
  - xAI
  - Grok
  - Roo Code
  - AI 模型
  - 推理 AI
  - 视觉模型
  - 大上下文
  - Grok Code Fast
  - Grok-4
  - Grok-3
  - Grok-2
  - 提示缓存
image: /img/social-share.jpg
sidebar_label: xAI (Grok)
---

# 在 Roo Code 中使用 xAI (Grok)

xAI 是 Grok 背后的公司，Grok 是一个以其对话能力和大上下文窗口而闻名的大型语言模型。Grok 模型旨在提供有用、信息丰富且上下文相关的回复。

**网站：** [https://x.ai/](https://x.ai/)

---

## 获取 API 密钥

1.  **注册/登录：** 访问 [xAI 控制台](https://console.x.ai/)。创建账户或登录。
2.  **导航到 API 密钥：** 进入仪表盘中的 API 密钥部分。
3.  **创建密钥：** 点击创建新的 API 密钥。为密钥起一个描述性的名称（例如 "Roo Code"）。
4.  **复制密钥：** **重要：** 立即复制 API 密钥。之后将无法再次查看。请安全存储。

---

## 可用模型

Roo Code 支持通过 xAI API 提供的所有 Grok 模型。

有关完整、最新的模型列表和功能，请参阅 [xAI 文档](https://docs.x.ai/docs)。

:::info Grok Code Fast - Roo Code 中的免费访问
`grok-code-fast-1` 在促销期间可通过 [Roo Code Cloud 提供商](/providers/roo-code-cloud) 免费使用。当直接在 Roo Code 中使用 xAI 提供商时，将应用标准定价。此模型之前称为 "roo/sonic"，现已更名。如需在 Roo Code 中免费访问，请使用 Roo Code Cloud 提供商而非 xAI 提供商。
:::

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从 "API Provider" 下拉菜单中选择 "xAI"。
3.  **输入 API 密钥：** 将你的 xAI API 密钥粘贴到 "xAI API Key" 字段中。
4.  **选择模型：** 从 "Model" 下拉菜单中选择你想要的 Grok 模型。

---

## 推理能力

Grok 3 Mini 模型具备专门的推理能力，允许它们在回复前"思考"——对于复杂的问题解决任务特别有用。

### 支持推理的模型

多个 Grok 模型具备推理能力。但是，只有 Grok 3 Mini 模型支持可配置的推理努力控制：

* `grok-3-mini` - 支持推理努力控制
* `grok-3-mini-fast` - 支持推理努力控制

其他模型（`grok-code-fast-1`、`grok-4.1-fast`、`grok-4`、`grok-3`、`grok-3-fast`）具备推理能力，但不暴露 `reasoning_effort` 参数。

### 控制推理努力

使用支持推理的模型时，你可以通过 `reasoning_effort` 参数控制模型的思考程度：

* `low`：最少的思考时间，使用更少的 token 以获得快速响应
* `high`：最大的思考时间，利用更多 token 解决复杂问题

对于应该快速完成的简单查询选择 `low`，对于响应延迟不那么重要的复杂问题选择 `high`。

### 主要特性

* **逐步问题解决**：模型在给出答案前会系统地思考问题
* **数学与量化优势**：在数值挑战和逻辑谜题方面表现出色
* **推理轨迹访问**：模型的思考过程可通过响应完成对象中的 `reasoning_content` 字段获得

---

## 提示缓存

提示缓存功能适用于选定的 Grok 模型，包括 `grok-code-fast-1`、`grok-4`、`grok-3`、`grok-3-fast`、`grok-3-mini` 和 `grok-3-mini-fast`。此功能可降低成本并提高响应速度。

---

## 定价

定价因模型而异。请参考 [xAI 文档](https://console.x.ai/) 了解当前定价信息。

**注意：** `grok-code-fast-1` 在促销期间可通过 [Roo Code Cloud 提供商](/providers/roo-code-cloud) 免费使用。当直接在 Roo Code 中使用 xAI 提供商时，将应用标准定价。