---
sidebar_label: 'Footgun Prompting'
description: Roo Code 中覆盖系统提示的高级指南。学习如何谨慎地使用系统提示覆盖来自定义 AI 行为。
keywords:
  - footgun prompting
  - system prompt override
  - advanced customization
  - Roo Code configuration
  - custom prompts
---

# Footgun Prompting：覆盖系统提示

Footgun Prompting（系统提示覆盖）允许您替换特定 Roo Code 模式的默认系统提示。这提供了细粒度控制，但会绕过内置保护机制。请谨慎使用。

<img src="/img/footgun-prompting/footgun-prompting-1.png" alt="活动系统提示覆盖的警告指示器" width="600" />
**警告指示器：** 当当前模式的系统提示覆盖处于活动状态时，Roo Code 将在聊天输入区域显示一个警告图标，提醒您默认行为已被修改。

:::info **footgun** _(名词)_

1.  _(编程俚语，幽默，贬义)_ 任何可能导致程序员搬起石头砸自己脚的功能。

> 系统提示覆盖被认为是一个 footgun，因为在不深入了解的情况下修改核心指令可能会导致意外或损坏的行为，尤其是在工具使用和响应一致性方面。

:::

---

## 工作原理

1.  **覆盖文件：** 在工作区根目录创建一个名为 `.roo/system-prompt-{mode-slug}` 的文件（例如，对于 Code 模式，创建 `.roo/system-prompt-code`）。
2.  **内容：** 此文件的内容将成为该特定模式的新系统提示。
3.  **激活：** Roo Code 会自动检测此文件。当存在时，它会替换大部分标准系统提示部分。
4.  **保留部分：** 只有核心的 `roleDefinition` 以及您为该模式设置的任何 `customInstructions` 会与您的覆盖内容一起保留。工具描述、规则和能力等标准部分将被绕过。
5.  **构建：** 发送给模型的最终提示如下所示：

    ```
    ${roleDefinition}

    ${content_of_your_override_file}

    ${customInstructions}
    ```

---

## 访问此功能

在 Roo Code UI 中找到选项和说明：

1.  点击 Roo Code 顶部菜单栏中的 <Codicon name="notebook" /> 图标。
2.  展开 **"高级：覆盖系统提示"** 部分。
3.  点击说明中的文件路径链接将在 VS Code 中打开或创建当前所选模式的正确覆盖文件。

<img src="/img/footgun-prompting/footgun-prompting.png" alt="显示“高级：覆盖系统提示”部分的 UI" width="500" />

---

## 使用上下文变量

在创建自定义系统提示文件时，您可以使用特殊变量（占位符），Roo Code 会自动将这些变量替换为有关当前环境的相关信息。这允许您使提示更具动态性和上下文感知能力。

以下是可用变量：

- `{{mode}}`：当前使用的 Roo Code 模式的 slug（短名称）（例如，`code`，`chat-mode`）。
- `{{language}}`：VS Code 中配置的显示语言（例如，`en`，`es`）。
- `{{shell}}`：VS Code 中配置的默认终端 shell（例如，`/bin/bash`，`powershell.exe`）。
- `{{operatingSystem}}`：您的计算机运行的操作系统类型（例如，`Linux`，macOS 的 `Darwin`，`Windows_NT`）。
- `{{workspace}}`：当前项目工作区根目录的文件路径。

**使用示例：**

您可以像这样直接在提示文件内容中包含这些变量：

```
您正在以“{{mode}}”模式协助用户。
他们的操作系统是 {{operatingSystem}}，默认 shell 是 {{shell}}。
项目位于：{{workspace}}。
请用 {{language}} 回答。
```

Roo Code 会在将提示发送给模型之前替换这些占位符。

---

## 关键注意事项和警告

- **目标受众：** 最适合对 Roo Code 的提示系统以及修改核心指令的影响非常熟悉的用户。
- **对功能的影响：** 自定义提示会覆盖标准指令，包括工具使用和响应一致性的指令。如果管理不当，这可能会导致意外行为或错误。
- **特定于模式：** 每个覆盖文件仅适用于其文件名中指定的模式（`{mode-slug}`）。
- **无文件，无覆盖：** 如果 `.roo/system-prompt-{mode-slug}` 文件不存在，Roo Code 将使用该模式的标准系统提示生成过程。
- **忽略空白文件：** 如果覆盖文件存在但为空（空白），它将被忽略，并将使用默认系统提示。
- **目录创建：** Roo Code 确保在尝试读取或创建覆盖文件之前 `.roo` 目录存在。
请谨慎使用此功能。错误的实现可能会显著降低受影响模式的 Roo Code 性能和可靠性。