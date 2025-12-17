---
description: 探索高效使用 Roo Code 的专家技巧和窍门。学习最佳实践、效率技巧和高级技术。
keywords:
  - Roo Code 技巧
  - 效率技巧
  - 最佳实践
  - AI 编程技巧
  - 高级技术
image: /img/social-share.jpg
---

# Tips & Tricks

一系列快速技巧，帮助你最大化 Roo Code 的使用效果。

- 将 Roo Code 拖到 [Secondary Sidebar](https://code.visualstudio.com/api/ux-guidelines/sidebars#secondary-sidebar) 中，这样你就能同时看到 Explorer、Search、Source Control 等。
<img src="/img/right-column-roo.gif" alt="将 Roo 放在右侧栏" width="900" />
- 一旦将 Roo Code 放在与文件浏览器分离的侧边栏中，你就可以将文件从浏览器直接拖入聊天窗口（甚至可以一次拖入多个文件）。只需确保在开始拖动文件后按住 Shift 键。
- 如果你没有使用 [MCP](/features/mcp/overview)，请在 <Codicon name="server" /> MCP Servers 标签页中将其关闭，以显著减少系统提示的大小。
- 为了让你的 [自定义模式](/features/custom-modes) 保持在正轨上，限制它们可以编辑的文件类型。
- 如果遇到令人头疼的 `input length and max tokens exceed context limit` 错误，你可以通过删除消息、回滚到之前的检查点，或切换到具有长上下文窗口的模型（如 Gemini）来恢复。
- 一般来说，对推理模型的 `Max Tokens` 设置要保持谨慎。每分配一个 token 给推理，就会减少可用于存储对话历史的空间。考虑仅在 Architect 和 Debug 模式下使用较高的 `Max Tokens` / `Max Thinking Tokens` 设置，而将 Code 模式保持在 16k max tokens 或更少。
- 如果有一个现实世界的工作招聘启事描述了你希望自定义模式完成的任务，尝试让 Code 模式 `Create a custom mode based on the job posting at @[url]`。
- 如果你想真正加速开发，可以检出多个代码仓库副本，并在所有副本上并行运行 Roo Code（使用 git 来解决冲突，就像处理人类开发者一样）。
- 使用 Debug 模式时，让 Roo "在 Debug 模式下开始一个新任务，包含解决 X 所需的所有必要上下文"，这样调试过程会使用自己的上下文窗口，不会污染主任务。
- 点击下方的 "Edit this page" 添加你自己的技巧！
- 为了管理大文件并减少上下文/资源使用，请调整 `File read auto-truncate threshold` 设置。此设置控制一次批量读取文件的行数。较低的值可以提高处理超大文件时的性能，但可能需要更多的读取操作。你可以在 Roo Code 设置的 'Advanced Settings' 下找到此设置。
- 为 [`roo.acceptInput` 命令](/features/keyboard-shortcuts) 设置键盘快捷键，无需鼠标即可接受建议或提交文本输入。非常适合键盘优先的工作流，减少手部疲劳。
- 使用 **Sticky Models** 为不同模式分配专业的人工智能模型（推理模型用于规划，非推理模型用于编码）。Roo 会自动切换到每个模式最后使用的模型，无需手动选择。
- 自定义 [上下文压缩提示](/features/intelligent-context-condensing#customizing-the-context-condensing-prompt)，如果你发现对于你的领域/用例它会忘记特定信息。你可以指示它保留对你工作流至关重要的特定类型信息。