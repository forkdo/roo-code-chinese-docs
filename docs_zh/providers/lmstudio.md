---
sidebar_label: LM Studio
description: 了解如何在 Roo Code 中设置和使用 LM Studio，通过 OpenAI 兼容的 API 支持运行本地语言模型。
keywords:
  - LM Studio
  - 本地模型
  - Roo Code
  - AI 集成
  - GGUF 模型
  - CodeLlama
  - Mistral
  - DeepSeek
  - 本地推理
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 LM Studio

Roo Code 支持使用 LM Studio 运行本地模型。LM Studio 提供了一个用户友好的界面，用于下载、配置和运行本地语言模型。它还内置了一个本地推理服务器，可模拟 OpenAI API，便于与 Roo Code 集成。

**官网：** [https://lmstudio.ai/](https://lmstudio.ai/)

---

## 设置 LM Studio

1.  **下载并安装 LM Studio：** 从 [LM Studio 官网](https://lmstudio.ai/) 下载并安装 LM Studio。
2.  **下载模型：** 使用 LM Studio 界面搜索并下载 GGUF 格式的模型。你可以在 LM Studio 的搜索界面中浏览所有可用模型，或访问 [Hugging Face](https://huggingface.co/models?library=gguf)。
3.  **启动本地服务器：**
    *   打开 LM Studio。
    *   点击 **"Local Server"** 标签（图标为 `<->`）。
    *   选择你下载的模型。
    *   点击 **"Start Server"**。

---

## 在 Roo Code 中的配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从 "API Provider" 下拉菜单中选择 "LM Studio"。
3.  **输入模型 ID：** 输入你在 LM Studio 中加载的模型的*文件名*（例如 `codellama-7b.Q4_0.gguf`）。你可以在 LM Studio 的 "Local Server" 标签中找到该文件名。
4.  **（可选）Base URL：** 默认情况下，Roo Code 将连接到 `http://localhost:1234` 上的 LM Studio。如果你将 LM Studio 配置为使用不同的地址或端口，请在此处输入完整 URL。

---

## 提示与注意事项

*   **资源需求：** 在本地运行大型语言模型可能非常消耗资源。请确保你的计算机满足所选模型的最低要求。
*   **模型选择：** LM Studio 提供了多种模型。请尝试选择最适合你需求的模型。
*   **本地服务器：** LM Studio 本地服务器必须处于运行状态，Roo Code 才能连接。
*   **LM Studio 文档：** 更多信息请参考 [LM Studio 文档](https://lmstudio.ai/docs)。
*   **故障排除：** 如果看到 "Please check the LM Studio developer logs to debug what went wrong" 错误，你可能需要调整 LM Studio 中的上下文长度设置。
*   **Token 跟踪：** Roo Code 会跟踪通过 LM Studio 运行的模型的 Token 使用情况，帮助你监控消耗。
*   **推理支持：** 对于支持的模型，Roo Code 可以解析 LM Studio 响应中的 "think" 标签或类似的推理指示器，提供对模型处理过程的更多洞察。