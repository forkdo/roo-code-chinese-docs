---
sidebar_label: OpenAI Compatible
description: 将 Roo Code 与任何 OpenAI 兼容的 API 提供商配合使用，包括 Perplexity、Together AI、Anyscale 和自定义端点。
keywords:
  - OpenAI compatible
  - Roo Code
  - API integration
  - custom endpoints
  - Together AI
  - Perplexity
  - Anyscale
  - model configuration
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 OpenAI 兼容提供商

Roo Code 支持多种 AI 模型提供商，这些提供商提供与 OpenAI API 标准兼容的 API。这意味着您可以使用来自 *非* OpenAI 的提供商的模型，同时仍使用熟悉的 API 接口。这包括以下提供商：

*   **本地模型**，通过 Ollama 和 LM Studio 等工具运行（在单独的部分中介绍）。
*   **云提供商**，如 Perplexity、Together AI、Anyscale 等。
*   **任何其他**提供 OpenAI 兼容 API 端点的提供商。

本文档重点介绍如何配置 *非* 官方 OpenAI API 的提供商（官方 OpenAI API 有其自己的[专用配置页面](/providers/openai)）。

---

## 通用配置

使用 OpenAI 兼容提供商的关键是配置两个主要设置：

1.  **Base URL**：这是提供商的 API 端点。它 *不会* 是 `https://api.openai.com/v1`（那是官方 OpenAI API 的地址）。
2.  **API Key**：这是您从提供商处获得的密钥。
3.  **Model ID**：这是特定模型的模型名称。

您可以在 Roo Code 设置面板中找到这些设置（点击 <Codicon name="gear" /> 图标）：

*   **API Provider**：选择 "OpenAI Compatible"。
*   **Base URL**：输入您选择的提供商提供的基础 URL。**这很关键**。
*   **API Key**：输入您的 API 密钥。
*   **Model**：选择一个模型。
*   **Model Configuration**：这允许您自定义模型的高级配置
    - Max Output Tokens
    - Context Window
    - Image Support
    - Computer Use
    - Input Price
    - Output Price

---

## 原生工具调用（OpenAI-Native 端点）

当您将此提供商直接连接到官方 OpenAI API（或完全镜像它的端点）时，Roo Code 可以使用 OpenAI 的**原生工具调用**协议，而不是基于 XML 的工具格式。

总体而言：

- **工具定义**使用 OpenAI 的原生工具架构发送给模型。
- **工具调用**作为专用工具事件流式返回，包括工具名称、参数和元数据。
- **工具参数**是增量流式传输的，这减少了模型决定使用工具和 Roo Code 执行工具之间的延迟。

### 原生工具的使用场景

当**所有**以下条件都满足时，Roo Code 才会使用原生工具调用：

1. 所选提供商已为 OpenAI 原生协议配置（OpenAI 或完全支持原生工具的 OpenAI 兼容端点）。
2. 活动配置文件的工具协议设置为允许原生工具（或保持默认值，即在支持时优先使用原生工具）。
3. 所选模型支持原生工具调用。

如果这些条件中有任何一项不满足，Roo Code 将回退到其基于 XML 的工具协议。

### 示例：简单的原生工具流程

以下是一个简化的示例，展示当使用 OpenAI 原生端点时，文件读取工具可能如何暴露：

```json
{
  "tools": [
    {
      "type": "function",
      "function": {
        "name": "read_file",
        "description": "Read a file from the workspace with line numbers.",
        "parameters": {
          "type": "object",
          "properties": {
            "path": { "type": "string", "description": "Relative file path" },
            "start_line": { "type": "integer", "nullable": true },
            "end_line": { "type": "integer", "nullable": true }
          },
          "required": ["path"]
        }
      }
    }
  ]
}
```

当模型决定使用 `read_file` 时，Roo Code 会在任务时间线中显示**流式工具事件**：

- 一个原生的*工具调用*事件，包含工具名称和正在生成的参数
- 相应的*工具结果*事件，显示文件内容以及任何截断或行范围信息

这为您提供更低延迟的反馈，了解正在使用哪些工具以及使用了哪些参数。

### 设置和限制

- **工具协议选择器**：在高级设置中，您可以选择 Roo Code 应该优先使用的工具协议（XML 与原生）。如果您在此处禁用原生工具，即使提供商支持原生工具，Roo Code 也总是使用 XML。
- **模型支持**：并非所有 OpenAI 原生或兼容模型都支持工具。如果模型不支持工具，Roo Code 将不会尝试为其发送工具定义。
- **提供商差异**：一些 OpenAI 兼容提供商仅部分实现了原生工具 API。如果 Roo Code 检测到协议错误，可能会自动回退到 XML 工具。

有关 Roo Code 中工具工作原理的更深入概述，请参阅[工具使用概述](/advanced-usage/available-tools/tool-use-overview)。

---

## 故障排除

*   **"Invalid API Key"**：仔细检查您是否正确输入了 API 密钥。
*   **"Model Not Found"**：确保您使用的是所选提供商的有效模型 ID。
*   **Connection Errors**：验证 Base URL 是否正确，以及您的提供商的 API 是否可访问。
*   **Unexpected Results**：如果您得到意外结果，请尝试使用不同的模型。

通过使用 OpenAI 兼容提供商，您可以利用 Roo Code 的灵活性，使用更广泛的 AI 模型。请记住，始终查阅您提供商的文档，以获取最准确和最新的信息。