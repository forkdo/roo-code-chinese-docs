---
sidebar_label: OpenAI
description: 将 Roo Code 连接到 OpenAI 官方 API，访问 GPT 和推理模型，支持高级功能和详细程度控制。
keywords:
  - OpenAI
  - GPT 模型
  - 推理模型
  - Roo Code
  - AI 集成
  - API 密钥
  - OpenAI 官方 API
  - 详细程度
  - 推理努力
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 OpenAI

Roo Code 支持通过 OpenAI 官方 API 直接访问模型，包括最新的 GPT-5 系列，具备推理努力控制和详细程度设置等高级功能。

**官网：** [https://openai.com/](https://openai.com/)

---

## 获取 API 密钥

1.  **注册/登录：** 访问 [OpenAI 平台](https://platform.openai.com/)。创建账户或登录。
2.  **导航到 API 密钥：** 访问 [API 密钥](https://platform.openai.com/api-keys) 页面。
3.  **创建密钥：** 点击“创建新密钥”。为密钥输入描述性名称（例如“Roo Code”）。
4.  **复制密钥：** **重要：** 立即复制 API 密钥。您将无法再次查看它。请安全存储。

---

## 可用模型

Roo Code 支持 OpenAI API 提供的所有模型。

有关完整、最新的模型列表和功能，请参阅 [OpenAI 模型文档](https://platform.openai.com/docs/models)。

---

## 在 Roo Code 中配置

### 设置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“OpenAI”。
3.  **输入 API 密钥：** 将您的 OpenAI API 密钥粘贴到“OpenAI API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择您需要的模型。
5.  **（可选）基础 URL：** 如果需要使用自定义基础 URL，请输入 URL。大多数人无需调整此项。

---

## 高级功能

### 推理努力控制

对于支持推理的模型（GPT-5、o1、o3、o4 系列），您可以控制模型的思考深度：

**GPT-5 模型：**
- `minimal` - 快速响应，基础推理
- `low` - 快速响应，轻度推理
- `medium`（默认）- 平衡推理和响应时间
- `high` - 深度推理，解决复杂问题

**o1/o3/o4 模型：**
- `low` - 最小思考时间
- `medium` - 平衡方法
- `high` - 最大思考，解决复杂问题

某些模型具有固定的推理级别，无法更改。

### 详细程度控制

适用于 GPT-5 模型和部分其他模型，详细程度控制响应的详细级别：

- `low` - 简洁、直接的响应
- `medium`（默认）- 平衡详细程度
- `high` - 全面、详细的响应

### 温度设置

温度控制输出随机性（0.0 到 2.0）：

- **GPT-5 模型：** 默认 1.0，平衡创造性
- **其他模型：** 默认 0.0，确定性输出
- **注意：** o1/o3 推理模型不支持

### 对话连续性（GPT-5）

GPT-5 模型通过响应 ID 高效维护对话上下文，减少令牌使用量的同时保持上下文。此功能自动生效，无需配置。

---

## 提示和说明

*   **定价：** 请参阅 [OpenAI 定价](https://openai.com/pricing) 页面，了解当前模型成本和折扣，包括提示缓存。
*   **Azure OpenAI 服务：** 如果您想使用 Azure OpenAI 服务，请参阅我们的 [OpenAI 兼容](/providers/openai-compatible) 提供商部分。
*   **上下文优化：** 对于 GPT-5-Codex，通过在请求间保持一致的上下文利用提示缓存，显著降低成本。