---
sidebar_label: 连接 AI 提供商
description: 了解如何将 Roo Code 连接到 Anthropic Claude、OpenAI 和 OpenRouter 等 AI 提供商。提供 API 密钥设置和配置的分步指南。
keywords:
  - Roo Code API 密钥
  - Claude API
  - OpenAI API
  - OpenRouter
  - Anthropic API
  - AI 提供商设置
  - API 配置
image: /img/social-share.jpg
---
import KangarooIcon from '@site/src/components/KangarooIcon';

# 连接你的第一个 LLM 提供商

Roo Code 需要一个推理提供商来访问使其正常工作的 LLM 模型。

一个很好的起点是 **Claude Sonnet 4.5**，它在合理的价格点上提供了强大的功能。要开始使用，请选择一个提供商：

- **Roo Code Cloud Provider（推荐）**：访问多个经过 Roo Code 测试的提供商的最简单方式。无需 API 密钥。只需选择 Roo Code Cloud 作为提供商并按照说明操作即可。[了解更多](/roo-code-provider/overview)。

- **OpenRouter**：通过单个 API 密钥提供对来自不同实验室的多种 AI 模型的访问。非常适合灵活性和快速上手。要获取 API 密钥，[请按照这些说明操作 <LucideIcon name="ArrowRight" />](/providers/openrouter#getting-an-api-key)

- **Anthropic**：直接访问 Claude 系列模型。需要 API 访问权限批准，并且根据你的层级可能有[速率限制](https://docs.anthropic.com/en/api/rate-limits#requirements-to-advance-tier)。要获取 API 密钥，[请按照这些说明操作 <LucideIcon name="ArrowRight" />](/providers/anthropic#getting-an-api-key)

Roo Code 与[其他提供商](/providers)兼容，这些提供商提供 Claude 以及你可以尝试的各种不同模型。

:::info 模型选择建议
我们推荐 **Claude Sonnet 4.5**，因为它对大多数任务来说“开箱即用”。我们在内部大量使用它。

你可以选择其他模型，但这会增加复杂性。不同的模型在遵循工具指令、解析格式以及在多步骤操作中保持上下文方面有所不同，因此最好稍后再尝试它们。如果你确实想尝试其他模型，请选择专门设计用于结构化推理和工具使用的模型。
:::

---

## 在 VS Code 中配置提供商

1. 点击 VS Code 活动栏中的 Roo Code 图标 (<KangarooIcon />) 打开 Roo Code 面板
2. 在欢迎界面中，选择你的 LLM 提供商
3. 如果你选择 Roo Code Cloud 提供商，只需连接你的账户并从下拉菜单中选择 `anthropic/claude-sonnet-4-5`。完成配置
4. 如果你选择了其他提供商，将从提供商处复制的 API 密钥粘贴到相应字段中并继续
5. 选择你的模型（应该显示为 `claude-sonnet-4-5` 或 `anthropic/claude-sonnet-4-5`）并完成流程

现在你可以开始编码了！