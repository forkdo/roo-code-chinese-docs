---
description: Find answers to common questions about Roo Code, including setup, usage, troubleshooting, and advanced features. Get help with API keys, modes, and more.
keywords:
  - Roo Code FAQ
  - frequently asked questions
  - troubleshooting
  - API setup
  - custom modes
  - MCP
  - local models
image: /img/social-share.jpg
---

import KangarooIcon from '@site/src/components/KangarooIcon';

# 常见问题解答

本页面回答了关于 Roo Code 的一些常见问题。

---

## 一般问题

### 什么是 Roo Code？

Roo Code 是一套由 AI 驱动的编码产品套件，旨在充分利用最先进的大语言模型。

### Roo Code 是如何工作的？

Roo Code 使用大语言模型（LLM）来理解您的请求，并将其转化为操作。它可以：

- 读取和写入您项目中的文件
- 执行 Shell 命令
- 执行网页浏览（如果启用）
- 通过模型上下文协议（MCP）使用外部工具

您可以通过聊天界面（在扩展中）或通过不同的通道（在云端）与 Roo Code 交互。

### Roo Code 能做什么？

Roo Code 可以帮助完成各种编码任务，包括：

*   根据自然语言描述生成代码
*   重构现有代码
*   修复 Bug
*   编写文档
*   解释代码
*   回答关于您代码库的问题
*   自动化重复性任务
*   创建新文件和项目

### Roo Code 是免费使用的吗？

Roo Code 扩展是免费且[开源](https://github.com/RooCodeInc/Roo-Code/)的。
Roo Code 云平台也是免费的，但某些功能需要付费。

在这两种情况下，Roo Code 都依赖于外部 LLM 推理提供商（如 [Anthropic](providers/anthropic)、[OpenAI](providers/openai)、[OpenRouter](providers/openrouter)、[Requesty](providers/requesty) 等）来提供 AI 能力。我们还提供[自己的提供商](/roo-code-provider/overview)作为替代方案。
这些提供商通常根据处理的令牌数量收取 API 使用费。您需要创建账户并从您选择的提供商处获取 API 密钥。详细了解[提供商及其设置方法](/providers/)。

### 使用 Roo Code 有哪些风险？

Roo Code 是一个强大的工具，使用时需要负责任。以下是一些需要注意的事项：

*   **Roo Code 可能会出错。** 在批准 Roo Code 的建议更改之前，请务必仔细审查。
*   **Roo Code 可以执行命令。** 请谨慎允许 Roo Code 运行命令，特别是如果您启用了自动批准。
*   **Roo Code 可以访问互联网。** 如果您使用支持网页浏览的提供商，请注意 Roo Code 可能会访问敏感信息。

---

## 设置与安装

### 如何安装 Roo Code？

请参阅[安装指南](/getting-started/installing)获取详细说明。

### 支持哪些 API 提供商？

请参阅[此处的完整列表](/providers/)。

### 如何获取 API 密钥？

每个 API 提供商都有自己的获取 API 密钥的流程。请参阅[设置您的第一个 AI 提供商](/getting-started/connecting-api-provider)以获取每个提供商相关文档的链接。

如果您使用 [Roo Code 云提供商](/roo-code-provider/overview)，则不需要 API 密钥。

### Roo Code 可以使用本地模型吗？
可以，Roo Code 支持使用 [Ollama](/providers/ollama) 和 [LM Studio](/providers/lmstudio) 在本地运行模型。请参阅[使用本地模型](/advanced-usage/local-models)获取说明。

---

## 扩展使用

### 如何开始新任务？
打开 Roo Code 面板（<KangarooIcon />），在聊天框中输入您的任务。清楚且具体地说明您希望 Roo Code 执行的操作。请参阅[键入您的请求](/basic-usage/typing-your-requests)以了解最佳实践。

### Roo Code 中的模式是什么？
[模式](/basic-usage/using-modes)是 Roo Code 可以采用的不同角色，每个角色都有特定的重点和能力。内置模式包括：

*   **Code：** 用于通用编码任务。
*   **Architect：** 用于规划和技术领导。
*   **Ask：** 用于回答问题和提供信息。
*   **Debug：** 用于系统性问题诊断。
您还可以创建[自定义模式](/features/custom-modes)。

### 如何在模式之间切换？

使用聊天输入区域中的下拉菜单选择不同的模式，或使用 `/` 命令切换到特定模式。

### 什么是工具，如何使用它们？
[工具](/basic-usage/how-tools-work)是 Roo Code 与您的系统交互的方式。Roo Code 会自动选择并使用适当的工具来完成您的任务。您不需要直接调用工具。您将被提示批准或拒绝每次工具使用。

### 什么是上下文引用？
[上下文引用](/basic-usage/context-mentions)是一种向 Roo Code 提供有关您项目的特定信息的方式，例如文件、文件夹或问题。使用 `@` 符号后跟您要引用的项目（例如 `@/src/file.ts`、`@problems`）。

### Roo Code 可以访问互联网吗？

是的，如果您使用的是支持网页浏览的提供商和模型。请注意允许此功能的安全影响。

### Roo Code 可以在终端中运行命令吗？

是的，Roo Code 可以在您的 VS Code 终端中执行命令。除非您启用了命令的自动批准，否则在执行每个命令之前都会提示您批准。请谨慎自动批准命令。如果您在终端命令方面遇到问题，请参阅[Shell 集成指南](/features/shell-integration)以获取故障排除信息。

### 如何向 Roo Code 提供反馈？

您可以通过批准或拒绝 Roo Code 的建议操作来提供反馈。您还可以使用反馈字段提供额外反馈。

### 可以自定义 Roo Code 的行为吗？

是的，您可以通过多种方式自定义 Roo Code：

*   **自定义指令：** 提供适用于所有模式的通用指令，或特定于模式的指令。
*   **自定义模式：** 创建您自己的模式，具有定制的提示和一些工具权限。
*   **`.roorules` 文件：** 在您的项目中创建 `.roorules` 文件以提供额外的指导方针。
*   **设置：** 调整各种设置，例如自动批准、差异编辑等。

### Roo Code 有自动批准设置吗？
是的，Roo Code 有几个设置，启用后会自动批准操作。在此处[了解更多信息](/features/auto-approving-actions)。

---

## 高级功能

### 可以离线使用 Roo Code 吗？
可以，如果您使用[本地模型](/advanced-usage/local-models)。

### 什么是 MCP（模型上下文协议）？
[MCP](/features/mcp/overview) 是一种协议，允许 Roo Code 与外部服务器通信，通过自定义工具和资源扩展其功能。

### 可以创建自己的 MCP 服务器吗？

是的，您可以创建自己的 MCP 服务器，为 Roo Code 添加自定义功能。请参阅 [MCP 文档](https://github.com/modelcontextprotocol)了解详细信息。

### 什么是代码库索引？

[代码库索引](/features/codebase-indexing) 使用 AI 嵌入创建您项目的语义搜索索引。这使得 Roo Code 能够通过基于含义而非仅关键字查找相关代码来更好地理解和导航大型代码库。

### 代码库索引的费用是多少？

代码库索引需要 OpenAI API 密钥来生成嵌入，以及 Qdrant 向量数据库进行存储。费用取决于您的项目大小和使用的嵌入模型。初始索引是最昂贵的部分；后续更新是增量的，便宜得多。

---

## 故障排除

### Roo Code 没有响应。我该怎么办？

*   确保您的 API 密钥正确且未过期。
*   检查您的互联网连接。
*   检查您选择的 API 提供商的状态。
*   尝试重启 VS Code。
*   如果问题仍然存在，请在 [GitHub](https://github.com/RooCodeInc/Roo-Code/issues) 或 [Discord](https://discord.gg/roocode) 上报告问题。

### 我看到一条错误消息。这是什么意思？

错误消息应提供有关问题的一些信息。如果您不确定如何解决，请在 [Discord](https://discord.gg/roocode) 中寻求帮助。

### Roo Code 做了我不想要的更改。如何撤销它们？

Roo Code 使用 VS Code 内置的文件编辑功能。您可以使用标准的“撤销”命令（Ctrl/Cmd + Z）来撤销更改。此外，如果启用了实验性检查点，Roo 可以撤销对文件所做的更改。

### Roo Code 无法写入 Markdown 文件。哪里出错了？

如果 Roo Code 写入 `.md` 文件失败，并出现“Failed to open diff editor”或“write_to_file tool failed”等错误，这通常是由干扰文件编辑的 VS Code 扩展或设置引起的：

**常见原因：**
- 具有“保存时格式化”功能的扩展
- VS Code 设置默认在预览模式中打开 Markdown 文件
- Markdown Preview 扩展或类似的 Markdown 处理扩展

**解决方案：**
- 禁用任何在保存时自动格式化文件的扩展
- 从您的 VS Code `settings.json` 中移除这些设置：
  ```json
  "markdown.preview.openMarkdownLinks": "inPreview",
  "workbench.editorAssociations": {
    "*.md": "vscode.markdown.preview.editor"
  }
  ```
- 暂时禁用 Markdown 相关扩展以测试它们是否是问题的原因
- 更改后重启 VS Code