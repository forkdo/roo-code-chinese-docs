---
sidebar_label: 'Footgun Prompting'
description: 高级指南：在 Roo Code 中覆盖系统提示。了解如何使用系统提示覆盖来自定义 AI 行为。
keywords:
  - footgun prompting
  - system prompt override
  - advanced customization
  - Roo Code configuration
  - custom prompts
image: /img/social-share.jpg
---

# Footgun Prompting：覆盖系统提示

Footgun Prompting（系统提示覆盖）允许你为特定的 Roo Code 模式替换默认的系统提示。这提供了细粒度的控制，但会绕过内置的安全机制。请谨慎使用。

<img src="/img/footgun-prompting/footgun-prompting-1.png" alt="当前模式启用系统提示覆盖时的警告指示器" width="600" />
**警告指示器：** 当前模式启用了系统提示覆盖时，Roo Code 会在聊天输入区域显示一个警告图标，提醒你默认行为已被修改。


:::info **footgun** _（名词）_

1.  _（编程俚语，幽默、贬义）_ 任何可能导致程序员搬起石头砸自己的脚的功能。

> 系统提示覆盖被视为一种 footgun，因为如果不深入了解而修改核心指令，尤其是工具使用和响应一致性方面，可能会导致意外或错误的行为。

:::

---

## 工作原理

1.  **覆盖文件：** 在工作区根目录创建一个名为 `.roo/system-prompt-{mode-slug}` 的文件（例如，代码模式为 `.roo/system-prompt-code`）。
2.  **内容：** 该文件的内容将成为该特定模式的新系统提示。
3.  **激活：** Roo Code 会自动检测此文件。当文件存在时，它会替换大部分标准系统提示部分。
4.  **保留部分：** 仅保留核心 `roleDefinition` 和你为该模式设置的任何 `customInstructions`，与你的覆盖内容一起使用。标准部分（如工具描述、规则和功能）将被绕过。
5.  **构建：** 发送给模型的最终提示如下所示：

    ```
    ${roleDefinition}

    ${content_of_your_override_file}

    ${customInstructions}
    ```

---

## 如何使用此功能

在 Roo Code UI 中找到选项和说明：

1.  点击 Roo Code 顶部菜单栏中的 <Codicon name="notebook" /> 图标。
2.  展开 **"高级：覆盖系统提示"** 部分。
3.  点击说明中的文件路径链接，将在 VS Code 中为当前选择的模式打开或创建正确的覆盖文件。

<img src="/img/footgun-prompting/footgun-prompting.png" alt="显示高级：覆盖系统提示部分的 UI" width="500" />

---

## 使用上下文变量

创建自定义系统提示文件时，你可以使用特殊的变量（占位符），Roo Code 会自动将其替换为当前环境的相关信息。这使得你的提示更加动态和上下文感知。

可用变量如下：

- `{{mode}}`：当前使用的 Roo Code 模式的 slug（简短名称）（例如 `code`、`chat-mode`）。
- `{{language}}`：VS Code 中配置的显示语言（例如 `en`、`es`）。
- `{{shell}}`：VS Code 中配置的默认终端 shell（例如 `/bin/bash`、`powershell.exe`）。
- `{{operatingSystem}}`：计算机运行的操作系统类型（例如 `Linux`、`Darwin`（macOS）、`Windows_NT`）。
- `{{workspace}}`：当前项目工作区根目录的文件路径。

**示例用法：**

你可以在提示文件内容中直接包含这些变量，如下所示：

```
你正在协助用户使用 '{{mode}}' 模式。
用户的操作系统是 {{operatingSystem}}，默认 shell 是 {{shell}}。
项目位于：{{workspace}}。
请使用 {{language}} 回复。
```

Roo Code 会在将提示发送给模型之前替换这些占位符。

---

## 重要注意事项与警告

- **目标用户：** 适用于对 Roo Code 提示系统及其修改核心指令影响有深入了解的用户。
- **功能影响：** 自定义提示会覆盖标准指令，包括工具使用和响应一致性方面的指令。如果管理不当，可能会导致意外行为或错误。
- **模式特定：** 每个覆盖文件仅适用于其文件名中指定的模式（`{mode-slug}`）。
- **无文件即无覆盖：** 如果 `.roo/system-prompt-{mode-slug}` 文件不存在，Roo Code 将为该模式使用标准系统提示生成过程。
- **空白文件被忽略：** 如果覆盖文件存在但为空（空白），将被忽略，使用默认系统提示。
- **目录创建：** Roo Code 确保在尝试读取或创建覆盖文件之前 `.roo` 目录存在。
谨慎使用此功能。实现不当可能会显著降低 Roo Code 在受影响模式下的性能和可靠性。