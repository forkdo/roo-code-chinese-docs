---
sidebar_label: Claude Code
description: 通过官方 CLI 在 Roo Code 中访问 Claude AI 模型。无需 API 密钥，支持高级推理和透明的成本跟踪。
keywords:
  - claude code
  - claude cli
  - roo code
  - api provider
  - claude max
  - no api key
  - claude reasoning
  - claude thinking mode
image: /img/social-share.jpg
---

# Claude Code Provider

Claude Code Provider 允许你通过 Anthropic 官方的命令行工具（CLI）而非 Web API 来使用 Claude 模型。这让你可以直接从 Roo Code 访问你的 Claude Max 订阅。

:::info 设置说明
在使用 Claude Code Provider 之前，请确保完成以下步骤：

1.  **安装 Claude CLI**：从 [Anthropic 的文档](https://docs.anthropic.com/en/docs/claude-code/setup) 下载并安装官方命令行工具。
2.  **身份验证**：在终端中运行 `claude` 启动应用程序。启动后，在应用中输入 `/login` 登录你的 Anthropic 账户。此步骤是必需的，用于授予 Roo Code 访问你 Claude 订阅的权限。
3.  **验证设置**：通过运行 `claude --version` 确认 CLI 正常工作。这确保 Roo Code 能够找到并使用该可执行文件。
4.  **在 Roo Code 中配置**：
    *   进入 Roo Code 设置，选择 **"Claude Code"** 作为你的 API 提供商。
    *   如果你将 CLI 安装在自定义位置，请在 **"Claude Code Path"** 中设置为完整的可执行文件路径（例如 `/usr/local/bin/claude`）。否则可以留空。
    *   从可用选项中选择你想要的模型。

配置完成后，Roo Code 将使用你的本地 Claude CLI 安装与 Anthropic 的模型交互，利用你现有的订阅。
:::


:::warning 环境变量使用说明
`claude` 命令行工具与其他 Anthropic SDK 一样，可以使用 `ANTHROPIC_API_KEY` 环境变量进行身份验证。这是在非交互式环境中授权 CLI 工具的常用方法。

如果你的系统设置了此环境变量，`claude` 工具可能会使用它进行身份验证，而不是交互式的 `/login` 方法。当 Roo Code 执行该工具时，它会准确反映正在使用 API 密钥，因为这是 `claude` CLI 本身的底层行为。
:::

**官网**：[https://docs.anthropic.com/en/docs/claude-code/setup](https://docs.anthropic.com/en/docs/claude-code/setup)

---

## 工作原理

Claude Code Provider 的工作原理如下：

1. **运行命令**：使用你的提示执行 `claude` CLI 命令。
2. **处理输出**：通过高级解析处理 CLI 的分块 JSON 输出。
3. **处理推理**：在可用时捕获并显示 Claude 的思考过程。
4. **跟踪使用情况**：报告 CLI 提供的令牌使用量和成本。

该 Provider 与 Roo Code 的界面集成，让你获得与其他 Provider 相同的体验，同时在底层使用 Claude CLI。

---

## 配置

### **Claude Code Path**
- **设置**：`claudeCodePath`
- **说明**：Claude CLI 可执行文件的路径。
- **默认值**：`claude`（假设它在你的系统 PATH 中）。
- **何时修改**：如果你将 Claude CLI 安装在自定义位置。

**自定义路径示例**：
- macOS/Linux：`/usr/local/bin/claude` 或 `~/bin/claude`

### **Max Output Tokens**
- **默认值**：16,384 个令牌（16k）—— 从之前的 8k 默认值增加
- **环境变量**：`CLAUDE_CODE_MAX_OUTPUT_TOKENS`
- **说明**：控制 Claude 在单次响应中可以生成的最大令牌数。
- **何时修改**：如果你需要更长的响应，或想通过限制输出长度来控制成本/性能。

**配置示例**：
```bash
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=32768  # 设置为 32k 个令牌
```

---

## 可用模型

Claude Code Provider 支持通过官方 CLI 可用的所有 Claude 模型。

模型可用性取决于你的 Claude CLI 订阅和计划。详情请见 [Anthropic 的 CLI 文档](https://docs.anthropic.com/en/docs/claude-code/setup)。

---

## 输出令牌限制

Claude Code Provider 现在默认为 16,384（16k）最大输出令牌，允许更长、更完整的响应。这对以下场景特别有用：
- 生成大型代码文件
- 详细的解释和文档
- 复杂的重构操作
- 多文件更改

你可以使用 `CLAUDE_CODE_MAX_OUTPUT_TOKENS` 环境变量自定义此限制，以满足你的使用场景需求。

---

## 常见问题

**"我需要为这个 Provider 提供 Claude API 密钥吗？"**
- 通常不需要。你可以通过 `claude` 应用中的 `/login` 命令进行交互式身份验证。
- 但是，如果设置了 `ANTHROPIC_API_KEY` 环境变量，Claude CLI 可能会使用它进行身份验证。详情请见上方的警告说明。

**"如何安装 Claude CLI？"**
- 访问 [Anthropic 的 CLI 文档](https://docs.anthropic.com/en/docs/claude-code/setup) 获取安装说明
- CLI 会处理自己的身份验证和设置

**"为什么我要使用这个而不是常规的 Anthropic Provider？"**
- 根据你的订阅可能具有成本优势

**"如果 CLI 不在 PATH 中怎么办？"**
- 在 Claude Code Path 设置中设置自定义路径
- 指向你安装 CLI 的完整路径

