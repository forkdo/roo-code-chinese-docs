---
description: 通过实验性的 Language Model API 集成，在 Roo Code 中使用 GitHub Copilot 和其他 VS Code 语言模型。
keywords:
  - VS Code LM API
  - Language Model API
  - GitHub Copilot
  - Roo Code
  - VS Code extensions
  - AI models
  - experimental features
image: /img/social-share.jpg
sidebar_label: VS Code Language Model API
---

# 在 Roo Code 中使用 VS Code Language Model API

Roo Code 包含对 [VS Code Language Model API](https://code.visualstudio.com/api/extension-guides/language-model) 的*实验性*支持。该 API 允许扩展直接在 VS Code 内提供对语言模型的访问。这意味着你可以使用以下来源的模型：

*   **GitHub Copilot：** 如果你订阅了 Copilot 并安装了相应的扩展。
*   **其他 VS Code 扩展：** 任何实现了 Language Model API 的扩展。

**重要提示：** 此集成功能处于实验阶段，可能无法按预期工作。它依赖于其他扩展正确实现 VS Code Language Model API。

---

## 前置条件

*   **VS Code：** Language Model API 通过 VS Code 提供支持（目前不支持 Cursor）。
*   **语言模型提供者扩展：** 你需要一个提供语言模型的扩展。示例包括：
    *   **GitHub Copilot：** 如果你订阅了 Copilot，GitHub Copilot 和 GitHub Copilot Chat 扩展可以提供模型。
    *   **其他扩展：** 在 VS Code 市场中搜索提及 "Language Model API" 或 "lm" 的扩展。可能还有其他可用的实验性扩展。

---

## 配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供者：** 在 "API Provider" 下拉菜单中选择 "VS Code LM API"。
3.  **选择模型：** "Language Model" 下拉菜单将（最终）列出可用的模型。格式为 `vendor/family`。例如，如果你使用 Copilot，可能会看到类似 `copilot - <model-name>` 的选项。

---

## 限制

*   **实验性 API：** VS Code Language Model API 仍在开发中。请预期可能会有变更和不稳定性。
*   **依赖扩展：** 此功能完全依赖于其他扩展提供模型。Roo Code 无法直接控制哪些模型可用。
*   **功能有限：** VS Code Language Model API 可能不支持其他 API 提供者的所有功能（例如，图像输入、流式传输、详细的使用信息）。
*   **无直接成本控制：** 你受提供模型的扩展的定价和条款约束。Roo Code 无法直接跟踪或限制成本。
*   **GitHub Copilot 速率限制：** 当使用 VS Code LM API 和 GitHub Copilot 时，请注意 GitHub 可能对 Copilot 使用施加速率限制。这些限制由 GitHub 控制，而非 Roo Code。

---

## 故障排除

*   **未显示模型：**
    *   确保你已安装 VS Code。
    *   确保你已安装并启用了语言模型提供者扩展（例如，GitHub Copilot、GitHub Copilot Chat）。
    *   如果使用 Copilot，请确保你已使用想要的模型发送过 Copilot Chat 消息。
*   **意外行为：** 如果遇到意外行为，可能是底层 Language Model API 或提供者扩展的问题。请考虑向提供者扩展的开发者报告此问题。