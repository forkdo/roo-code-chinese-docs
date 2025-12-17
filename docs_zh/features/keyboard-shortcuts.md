---
description: 掌握 Roo Code 中的键盘导航，通过可自定义的快捷键、命令执行和提示历史导航，实现高效的编码工作流。
keywords:
  - keyboard shortcuts
  - keyboard navigation
  - roo-cline.acceptInput
  - prompt history
  - accessibility
  - vim compatibility
image: /img/social-share.jpg
sidebar_label: Keyboard Navigation
---

# 键盘导航

Roo Code 界面支持键盘导航和快捷键，帮助您优化工作流程，减少对鼠标操作的依赖。

---

## 可用的键盘命令

Roo Code 提供多种键盘命令来增强您的工作流程。本文档重点介绍 `roo-cline.acceptInput` 命令，但以下是所有键盘命令的快速参考：

| 命令 | 描述 | 默认快捷键 |
|---------|-------------|-----------------|
| `roo-cline.acceptInput` | 提交文本或接受主要建议 | 无（可自定义） |
| `roo-cline.focusInput` | 聚焦 Roo 输入框 | 无（可自定义） |
| Add to Context | 将选定的代码添加到 Roo 的上下文中 | macOS: Cmd+K Cmd+A; Windows/Linux: Ctrl+K Ctrl+A |
| 上/下箭头 | 导航提示历史记录 | 内置 |

### 键盘命令的关键优势

* **键盘驱动界面**：无需鼠标交互即可提交文本或选择主要建议按钮
* **提高可访问性**：对行动不便或使用鼠标时感到不适的用户至关重要
* **Vim/Neovim 兼容性**：支持来自以键盘为中心环境的开发者无缝过渡
* **工作流效率**：减少开发任务期间在键盘和鼠标之间切换的频率

---

## roo-cline.acceptInput 命令

`roo-cline.acceptInput` 命令允许您使用键盘快捷键提交文本或接受建议，而不是点击按钮或在输入区域按 Enter。

### 功能说明

`roo-cline.acceptInput` 命令是一个通用的输入提交命令。触发时，它会：

- 当在文本输入区域时，提交您当前的文本或图像输入（等同于按 Enter）
- 当显示操作按钮时（如确认/取消按钮或任何其他操作按钮），点击主要（第一个）按钮

### 详细设置指南

#### 方法 1：使用 VS Code UI

1. 打开命令面板（`Ctrl+Shift+P` 或 Mac 上的 `Cmd+Shift+P`）
2. 输入 "Preferences: Open Keyboard Shortcuts"
3. 在搜索框中输入 "roo-cline.acceptInput"
4. 在结果中找到 "Roo: Accept Input/Suggestion"
5. 点击命令左侧的 + 图标
6. 按下您想要的键组合（例如 `Ctrl+Enter` 或 `Alt+Enter`）
7. 按 Enter 确认

#### 方法 2：直接编辑 keybindings.json

1. 打开命令面板（`Ctrl+Shift+P` 或 Mac 上的 `Cmd+Shift+P`）
2. 输入 "Preferences: Open Keyboard Shortcuts (JSON)"
3. 在 JSON 数组中添加以下条目：

```json
{
  "key": "ctrl+enter",  // 或您偏好的键组合
  "command": "roo-cline.acceptInput",
  "when": "view == roo-cline.SidebarProvider || activeWebviewPanelId == roo-cline.TabPanelProvider"
}
```

作用域示例：
- 仅限侧边栏 Roo 视图：
```json
{
  "key": "ctrl+enter",
  "command": "roo-cline.acceptInput",
  "when": "view == roo-cline.SidebarProvider"
}
```
- 仅限编辑器 Roo 标签页：
```json
{
  "key": "ctrl+enter",
  "command": "roo-cline.acceptInput",
  "when": "activeWebviewPanelId == roo-cline.TabPanelProvider"
}
```

#### 推荐的键组合

选择不与现有 VS Code 快捷键冲突的键组合：

- `Alt+Enter` - 打字时易于按下
- `Ctrl+Space` - 对使用自动补全的用户来说很熟悉
- `Ctrl+Enter` - 直观地用于命令执行
- `Alt+A` - "Accept" 的助记符

## Add to Context 快捷键

- 默认值：macOS: Cmd+K Cmd+A; Windows/Linux: Ctrl+K Ctrl+A
- 要求：when 条件 `editorTextFocus && editorHasSelection`
- 焦点不会自动改变。要立即继续键入，请使用 "Roo: Focus Input" (`roo-cline.focusInput`) 或点击 Roo 面板。

:::note Redo 快捷键已恢复
标准的 Redo 快捷键（macOS: Cmd+Y; Windows/Linux: Ctrl+Y）保持不变，在 VS Code 中仍可正常使用。
:::

### 实际使用场景

#### 快速开发工作流

- **文本提交**：无需将手移开键盘即可向 Roo 发送消息
- **操作确认**：接受保存文件、运行命令或应用差异等操作
- **多步骤流程**：快速通过需要确认或输入的步骤
- **连续任务**：以最小的中断链接多个任务

#### 以键盘为中心的开发

- **Vim/Neovim 工作流**：如果您来自 Vim/Neovim 背景，可以保持以键盘为中心的工作流
- **IDE 集成**：与其他 VS Code 键盘快捷键配合使用，获得无缝体验
- **代码审查**：使用快捷键快速接受 Roo 的建议
- **文档编写**：生成文档时提交文本并接受格式建议

#### 可访问性使用场景

- **手部活动能力受限**：对难以使用鼠标用户至关重要
- **重复性劳损预防**：减少鼠标使用以预防或管理重复性劳损
- **屏幕阅读器集成**：与屏幕阅读器配合使用，方便视力障碍用户
- **语音控制兼容性**：与语音控制软件配合使用时可通过语音命令触发

### 可访问性优势

`roo-cline.acceptInput` 命令的设计考虑了可访问性：

- **减少鼠标依赖**：无需鼠标即可完成整个工作流
- **减轻身体压力**：帮助使用鼠标时感到不适或疼痛的用户
- **替代输入方法**：支持依赖键盘导航的行动障碍用户
- **工作流优化**：对来自以键盘为中心环境（如 Vim/Neovim）的用户特别有价值

### 以键盘为中心的工作流

以下是一些完整的使用示例，展示如何有效地将键盘快捷键与 Roo 配合使用：

#### 开发工作流示例

1. 打开 VS Code 并导航到您的项目
2. 通过侧边栏打开 Roo
3. 输入您的请求："为用户注册创建一个 REST API 端点"
4. 当 Roo 询问框架偏好时，使用您的 `roo-cline.acceptInput` 快捷键选择第一个建议
5. 继续使用快捷键接受代码生成建议
6. 当 Roo 提供保存文件时，再次使用快捷键确认
7. 使用 VS Code 的内置快捷键导航创建的文件

#### 代码审查工作流

1. 选择您要审查的代码并使用 VS Code 的 "Copy" 命令
2. 要求 Roo 审查："审查此代码的安全问题"
3. 当 Roo 就代码上下文询问澄清问题时，使用快捷键接受建议
4. 当 Roo 提供改进建议时，再次使用快捷键接受实施建议

### 故障排除

| 问题 | 解决方案 |
|-------|----------|
| 快捷键不工作 | 确保 Roo 已聚焦（先点击 Roo 面板） |
| 选择了错误的建议 | 该命令总是选择第一个（主要）按钮；如果需要其他选项，请使用鼠标 |
| 与现有快捷键冲突 | 在 VS Code 键盘设置中尝试不同的键组合 |
| 使用时没有视觉反馈 | 这是正常的 - 命令静默激活功能，没有视觉确认 |
| 快捷键工作不稳定 | 确保 `when` 子句正确配置（使用 `view == roo-cline.SidebarProvider` 或 `activeWebviewPanelId == roo-cline.TabPanelProvider`） |

### 技术实现

`roo-cline.acceptInput` 命令的实现如下：

- 命令注册为 `roo-cline.acceptInput`，在命令面板中显示标题为 "Roo: Accept Input/Suggestion"
- 触发时，它向活动的 Roo webview 发送 "acceptInput" 消息
- webview 根据当前 UI 状态确定适当的操作：
  - 如果操作按钮可见且启用，则点击主要操作按钮
  - 如果文本区域启用且包含文本/图像，则发送消息
- 无默认键绑定 - 用户分配首选快捷键

### 限制

- 仅在 Roo 界面处于活动状态时工作
- 如果当前没有可用的输入或建议，则无效
- 当显示多个选项时，优先选择主要（第一个）按钮

---

## 命令行风格的提示历史导航

使用箭头键以类似终端的体验导航您的提示历史。此功能让您可以轻松重用和优化之前的提示，无论是来自当前对话还是过去的任务。

### 主要功能
- **上/下箭头**：循环浏览以前的提示。
- **上下文感知**：在对话和任务历史之间切换。
- **保留输入**：记住您正在键入的内容。

### 为什么这很重要

**之前**：重用提示意味着向上滚动、复制和粘贴。
- 繁琐且缓慢
- 容易迷失方向
- 中断您的工作流

**使用提示历史导航后**：无需使用鼠标即可快速访问过去的提示。

### 工作原理

导航设计直观，能够适应您当前的上下文。

#### 在活跃对话中
- **上箭头**：显示您发送的最后一个提示。继续按可进一步回溯对话。
- **下箭头**：在对话历史中向前移动，最终返回您正在键入的文本。

#### 开始新聊天时
- **上箭头**：显示当前工作区中任务历史中最近的提示。
- **下箭头**：在您的任务历史中向前移动。

#### 边缘情况
- 如果您在导航时开始键入，历史记录会被取消，您输入的新文本会被保留。
- 导航仅在光标位于输入框的第一行或最后一行时有效，以避免干扰多行编辑。

### 配置

此功能默认启用。无需配置设置。

### 优势

- **更快的工作流**：无需鼠标即可重用提示。
- **更好的上下文**：轻松访问和构建以前的交互。
- **减少中断**：专注于手头的任务。

### 常见问题

**"为什么我按上箭头时没有反应？"**
- 您可能在多行提示的中间。光标必须在第一行。
- 当前上下文可能没有可用的历史记录。

**"对话历史和任务历史有什么区别？"**
- **对话历史** 包括您当前活跃聊天会话中的提示。
- **任务历史** 包括您当前工作区中所有先前任务的初始提示。