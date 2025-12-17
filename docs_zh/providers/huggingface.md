---
sidebar_label: Hugging Face
description: 将 Roo Code 连接到 Hugging Face 的推理路由服务，访问开源大语言模型。从多个推理提供商和模型（如 Llama、Mistral 等）中选择。
keywords:
  - hugging face
  - huggingface
  - roo code
  - api provider
  - open source models
  - llama
  - mistral
  - inference router
  - ai models
  - inference providers
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Hugging Face

Roo Code 与 Hugging Face 路由服务集成，提供对一系列精选开源模型的访问，这些模型经过优化，专为代码辅助场景设计。该集成允许你从多个推理提供商中选择，并自动选择最佳可用选项。

**官网：** [https://huggingface.co/](https://huggingface.co/)

---

## 获取 API 密钥

1. **注册/登录：** 访问 [Hugging Face](https://huggingface.co/) 并创建账户或登录。
2. **进入设置：** 点击你的头像，选择“Settings”（设置）。
3. **访问令牌：** 在设置中进入“Access Tokens”（访问令牌）部分。
4. **创建令牌：** 点击“New token”（新建令牌），并为其命名（例如“Roo Code”）。
5. **设置权限：** 选择“Read”（读取）权限（这对 Roo Code 已足够）。
6. **复制令牌：** **重要：** 立即复制该令牌，并安全保存。

---

## 可用模型

Roo Code 会自动从 Hugging Face 上精选的 'roocode' 集合中获取所有可用模型。

如需查看完整且最新的模型列表，请访问 [Hugging Face 的 roocode 集合](https://huggingface.co/collections/roocode)。

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 在“API Provider”（API 提供商）下拉菜单中选择“Hugging Face”。
3. **输入 API 密钥：** 将你的 Hugging Face API 令牌粘贴到“Hugging Face API Key”（Hugging Face API 密钥）字段中。
4. **选择模型：** 从“Model”（模型）下拉菜单中选择你想要的模型。下拉菜单会显示模型数量，且支持搜索。
5. **选择推理提供商（可选）：** 从下拉菜单中选择特定的推理提供商，或保持“Auto”（自动）模式（默认），以自动选择最佳可用提供商。

---

## 推理提供商选择

Hugging Face 的路由服务连接多个推理提供商。你可以：

- **自动模式（默认）：** 根据模型可用性和性能自动选择最佳可用提供商
- **手动选择：** 从下拉菜单中选择特定提供商

下拉菜单会显示每个提供商的状态：
- `live` - 提供商运行正常且可用
- `staging` - 提供商处于测试阶段
- `error` - 提供商当前遇到问题

提供商名称在 UI 中经过格式化处理，以提高可读性（例如，“sambanova” 显示为“SambaNova”）。

当你选择特定提供商时，模型能力（最大 token 数、价格）将更新为反映该提供商的特定配置。价格信息仅在选择特定提供商时显示，自动模式下不显示。

---

## 模型信息显示

对于每个选定的模型，Roo Code 会显示：

- **Max Output（最大输出）：** 模型可生成的最大 token 数（因提供商而异）
- **Pricing（价格）：** 每百万输入和输出 token 的成本（仅在选择特定提供商时显示）
- **Image Support（图像支持）：** 当前所有模型均显示为文本模式。这是 Roo Code 实现的限制，而非 Hugging Face API 的限制。

---

## 可用提供商

可用提供商列表是动态的，从 Hugging Face API 获取。常见提供商包括：

- **Together AI** - 高性能推理平台
- **Fireworks AI** - 快速且可扩展的模型服务
- **DeepInfra** - 成本效益高的 GPU 基础设施
- **Hyperbolic** - 优化的推理服务
- **Cerebras** - 硬件加速推理

*注意：上述提供商仅为常见选项的示例。实际列表可能有所不同。*

---

## 提示与说明

- **提供商故障转移：** 使用自动模式时，如果所选提供商失败，Hugging Face 基础设施将自动尝试其他可用提供商
- **速率限制：** 不同提供商可能有不同的速率限制和可用性
- **价格差异：** 同一模型在不同提供商之间的成本可能差异显著
- **模型更新：** roocode 集合会定期更新，包含新模型和改进版本