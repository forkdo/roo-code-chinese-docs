---
sidebar_label: Hugging Face
description: 将 Roo Code 连接到 Hugging Face 推理路由，以访问开源 LLM。可从多个推理提供商和模型（如 Llama、Mistral 等）中进行选择。
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
---

# 在 Roo Code 中使用 Hugging Face

Roo Code 与 Hugging Face 路由集成，提供对专为代码辅助优化的精选开源模型集合的访问。该集成允许您从多个推理提供商中进行选择，并自动选择最佳可用选项。

**网站：** [https://huggingface.co/](https://huggingface.co/)

---

## 获取 API 密钥

1. **注册/登录：** 访问 [Hugging Face](https://huggingface.co/) 并创建账户或登录。
2. **进入设置：** 点击您的头像，选择“Settings”（设置）。
3. **访问令牌：** 在设置中进入“Access Tokens”（访问令牌）部分。
4. **创建令牌：** 点击“New token”（新建令牌），并为其指定一个描述性名称（例如“Roo Code”）。
5. **设置权限：** 选择“Read”（读取）权限（这对 Roo Code 已足够）。
6. **复制令牌：** **重要：** 立即复制该令牌。请安全存储。

---

## 可用模型

Roo Code 会自动从 Hugging Face 上的精选 'roocode' 集合中获取所有可用模型。

要查看完整且最新的模型集合，请参阅 [Hugging Face 的 roocode 集合](https://huggingface.co/collections/roocode)。

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 从“API Provider”（API 提供商）下拉菜单中选择“Hugging Face”。
3. **输入 API 密钥：** 将您的 Hugging Face API 令牌粘贴到“Hugging Face API Key”（Hugging Face API 密钥）字段中。
4. **选择模型：** 从“Model”（模型）下拉菜单中选择您所需的模型。下拉菜单会显示模型数量，并支持搜索。
5. **选择推理提供商（可选）：** 从下拉菜单中选择一个特定的推理提供商，或保留为“Auto”（自动，默认），以自动选择最佳可用提供商。

---

## 推理提供商选择

Hugging Face 的路由会连接到多个推理提供商。您可以选择：

- **自动模式（默认）：** 根据模型可用性和性能自动选择最佳可用提供商
- **手动选择：** 从下拉菜单中选择特定提供商

下拉菜单会显示每个提供商的状态：
- `live` - 提供商运行正常且可用
- `staging` - 提供商处于测试阶段
- `error` - 提供商当前遇到问题

提供商名称在 UI 中进行了格式化以提高可读性（例如，“sambanova”显示为“SambaNova”）。

当您选择特定提供商时，模型能力（最大 token 数、定价）将更新以反映该提供商的具体配置。定价信息仅在选择了特定提供商时显示，自动模式下不显示。

---

## 模型信息显示

对于每个选定的模型，Roo Code 会显示：

- **最大输出：** 模型可生成的最大 token 数（因提供商而异）
- **定价：** 每百万输入和输出 token 的成本（仅在选择了特定提供商时显示）
- **图像支持：** 目前所有模型均显示为纯文本。这是 Roo Code 的实现限制，而非 Hugging Face API 的限制。

---

## 可用提供商

可用提供商的列表是动态的，并从 Hugging Face API 获取。常见提供商包括：

- **Together AI** - 高性能推理平台
- **Fireworks AI** - 快速且可扩展的模型服务
- **DeepInfra** - 经济高效的 GPU 基础设施
- **Hyperbolic** - 优化的推理服务
- **Cerebras** - 硬件加速推理

*注：上面列出的提供商是常见可用选项的示例。实际列表可能有所不同。*

---

## 提示和注意事项

- **提供商故障转移：** 使用自动模式时，如果选定的提供商失败，Hugging Face 的基础设施将自动尝试替代提供商
- **速率限制：** 不同提供商可能有不同的速率限制和可用性
- **定价差异：** 同一模型在不同提供商之间的成本可能有显著差异
- **模型更新：** roocode 集合会定期更新新的和改进的模型