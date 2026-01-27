---
sidebar_label: 兼容 OpenAI
description: 将 Roo Code 与任何兼容 OpenAI API 标准的提供商（包括 Perplexity、Together AI、Anyscale 以及自定义端点）配合使用。
keywords:
  - 兼容 OpenAI
  - Roo Code
  - API 集成
  - 自定义端点
  - Together AI
  - Perplexity
  - Anyscale
  - 模型配置
---

# 在 Roo Code 中使用兼容 OpenAI 的提供商

Roo Code 支持众多提供与 OpenAI API 标准兼容的 API 的 AI 模型提供商。这意味着您可以使用 *除* OpenAI 之外的提供商提供的模型，同时仍使用熟悉的 API 接口。这包括以下提供商：

*   通过 Ollama 和 LM Studio 等工具运行的**本地模型**（在单独的部分中介绍）。
*   **云提供商**，如 Perplexity、Together AI、Anyscale 等。
*   提供兼容 OpenAI API 端点的**任何其他提供商**。

本文档重点介绍如何设置 *除* 官方 OpenAI API 之外的提供商（官方 OpenAI API 有自己[专用的配置页面](/providers/openai)）。

---

## 通用配置

使用兼容 OpenAI 的提供商的关键在于配置两个主要设置：

1.  **基础 URL：** 这是提供商的 API 端点。它 *不会* 是 `https://api.openai.com/v1`（这是官方 OpenAI API 的地址）。
2.  **API 密钥：** 这是您从提供商处获得的密钥。
3.  **模型 ID：** 这是特定模型的名称。

您可以在 Roo Code 设置面板中找到这些设置（点击 <Codicon name="gear" /> 图标）：

*   **API 提供商：** 选择“兼容 OpenAI”。
*   **基础 URL：** 输入您选择的提供商提供的基础 URL。**这至关重要。**
*   **API 密钥：** 输入您的 API 密钥。
*   **模型：** 选择一个模型。
*   **模型配置：** 这允许您自定义模型的高级配置
    - 最大输出令牌数
    - 上下文窗口
    - 图像支持
    - 计算机使用
    - 输入价格
    - 输出价格

---

## 原生工具调用 (OpenAI 原生端点)

当您将此提供商直接连接到官方 OpenAI API（或完全镜像它的端点）时，Roo Code 可以使用 OpenAI 的**原生工具调用**协议，而不是基于 XML 的工具格式。

从高层次来看：

- **工具定义**使用 OpenAI 的原生工具架构发送给模型。
- **工具调用**作为专用工具事件流式传输回来，包括工具名称、参数和元数据。
- **工具参数**会逐步流式传输，这减少了模型决定使用工具与 Roo Code 执行工具之间的延迟。

### 何时使用原生工具

当**所有**以下条件都满足时，Roo Code 会使用原生工具调用：

1. 所选提供商配置为使用 OpenAI 原生协议（OpenAI 或完全支持原生工具的兼容 OpenAI 端点）。
2. 活动配置文件的工具协议设置为允许原生工具（或保持其默认设置，在支持时优先使用原生工具）。
3. 所选模型支持原生工具调用。

如果这些条件中的任何一个不满足，Roo Code 将回退到其基于 XML 的工具协议。

### 示例：简单的原生工具流程

以下是使用 OpenAI 原生端点时，文件读取工具可能如何暴露的简化示例：

```json
{
  "tools": [
    {
      "type": "function",
      "function": {
        "name": "read_file",
        "description": "从工作区读取带行号的文件。",
        "parameters": {
          "type": "object",
          "properties": {
            "path": { "type": "string", "description": "相对文件路径" },
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

当模型决定使用 `read_file` 时，Roo Code 会在任务时间线中显示**流式传输的工具事件**：

- 一个原生*工具调用*事件，其中包含正在生成的工具名称和参数
- 相应的*工具结果*事件，显示文件内容以及任何截断或行范围信息

这使您可以获得关于正在使用哪些工具以及使用什么参数的更低延迟反馈。

### 设置和限制

- **工具协议选择器：** 在高级设置中，您可以选择 Roo Code 应优先使用哪种工具协议（XML 与原生）。如果您在此处禁用原生工具，即使提供商支持原生工具，Roo Code 也将始终使用 XML。
- **模型支持：** 并非所有 OpenAI 原生或兼容模型都支持工具。如果模型不支持工具，Roo Code 将不会尝试为其发送工具定义。
- **提供商特性：** 一些兼容 OpenAI 的提供商仅部分实现原生工具 API。如果 Roo Code 检测到协议错误，它可能会自动回退到 XML 工具。

有关 Roo Code 中工具工作原理的更深入概述，请参阅[工具使用概述](/advanced-usage/available-tools/tool-use-overview)。

---

## 故障排除

*   **“无效的 API 密钥”：** 仔细检查您输入的 API 密钥是否正确。
*   **“找不到模型”：** 确保您使用的是您选择的提供商的有效模型 ID。
*   **连接错误：** 验证基础 URL 是否正确，以及您的提供商的 API 是否可访问。
*   **意外结果：** 如果您获得意外结果，请尝试不同的模型。

通过使用兼容 OpenAI 的提供商，您可以利用 Roo Code 的灵活性，与更广泛的 AI 模型一起使用。请务必始终查阅您的提供商的文档，以获取最准确和最新的信息。