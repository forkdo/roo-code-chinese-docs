---
description: 了解如何使用 .rooignore 文件控制 Roo Code 的文件访问，保护敏感信息，以及管理 AI 可以读取或修改的文件。
keywords:
  - rooignore
  - 文件访问控制
  - 敏感数据保护
  - gitignore 语法
  - 文件权限
  - 安全
image: /img/social-share.jpg
sidebar_label: .rooignore
---

# 使用 .rooignore 控制文件访问

`.rooignore` 文件是管理 Roo Code 与项目文件交互的核心功能。它允许你指定 Roo 不应访问或修改的文件和目录，类似于 `.gitignore` 对 Git 的作用。

---

## 什么是 `.rooignore`？

*   **用途**：保护敏感信息，防止意外修改构建产物或大型资源文件，并总体定义 Roo 在工作区中的操作范围。
*   **使用方法**：在 VS Code 工作区的根目录中创建一个名为 `.rooignore` 的文件。在此文件中列出模式，告诉 Roo 哪些文件和目录需要忽略。
*   **作用范围**：`.rooignore` 会影响 Roo 的工具和上下文引用（如 `@directory` 附件）。

Roo 会主动监控 `.rooignore` 文件。你所做的任何更改都会自动重新加载，确保 Roo 始终使用最新的规则。`.rooignore` 文件本身始终被隐式忽略，因此 Roo 无法更改自己的访问规则。

---

## 模式语法

`.rooignore` 的语法与 `.gitignore` 完全相同。以下是一些常见示例：

*   `node_modules/`：忽略整个 `node_modules` 目录。
*   `*.log`：忽略所有以 `.log` 结尾的文件。
*   `config/secrets.json`：忽略特定文件。
*   `!important.log`：例外情况；Roo 将*不会*忽略此特定文件，即使存在更广泛的模式（如 `*.log`）。
*   `build/`：忽略 `build` 目录。
*   `docs/**/*.md`：忽略 `docs` 目录及其子目录中的所有 Markdown 文件。

有关语法的完整指南，请参考 [Git 官方文档关于 .gitignore 的说明](https://git-scm.com/docs/gitignore)。

---

## Roo 工具如何与 `.rooignore` 交互

`.rooignore` 规则在各种 Roo 工具中得到强制执行：

### 严格执行（读取和写入）

这些工具在任何文件操作之前直接检查 `.rooignore`。如果文件被忽略，操作将被阻止：

*   [`read_file`](/advanced-usage/available-tools/read-file)：不会读取被忽略的文件。
*   [`write_to_file`](/advanced-usage/available-tools/write-to-file)：不会写入或创建新的被忽略文件。
*   [`apply_diff`](/advanced-usage/available-tools/apply-diff)：不会将差异应用到被忽略的文件。
*   [`list_code_definition_names`](/advanced-usage/available-tools/list-code-definition-names)：不会解析被忽略文件的代码符号。

### 文件发现和列出

*   **[`list_files`](/advanced-usage/available-tools/list-files) 工具和 `@directory` 附件**：当 Roo 列出文件或你使用 `@directory` 附件时，被忽略的文件会被省略或标记为 🔒 符号（见“用户体验”部分）。两者使用相同的过滤逻辑。
*   **环境详情**：提供给 Roo 的工作区信息（如打开的标签页和项目结构）经过过滤，排除或标记被忽略的项目。

### 上下文引用

*   **`@directory` 附件**：目录内容遵循 `.rooignore` 模式。被忽略的文件根据 `showRooIgnoredFiles` 设置被过滤掉或标记为 `[🔒]` 前缀。
*   **单文件引用**：被忽略的文件返回 "(File is ignored by .rooignore)" 而非内容。

### 命令执行

*   **[`execute_command`](/advanced-usage/available-tools/execute-command) 工具**：此工具检查命令（来自预定义列表，如 `cat` 或 `grep`）是否针对被忽略的文件。如果是，执行将被阻止。

---

## 关键限制和范围

*   **以工作区为中心**：`.rooignore` 规则**仅适用于当前 VS Code 工作区根目录内的文件和目录**。此范围外的文件不受影响。
*   **[`execute_command`](/advanced-usage/available-tools/execute-command) 特异性**：`execute_command` 的保护仅限于预定义的文件读取命令列表。自定义脚本或不常见的实用程序可能不会被捕获。
*   **非完整沙箱**：`.rooignore` 是控制 Roo 文件访问的强大工具，但它不会创建系统级沙箱。

---

## 用户体验和通知

*   **视觉提示 (🔒)**：在文件列表和 `@directory` 附件中，被 `.rooignore` 忽略的文件可能用锁符号 (🔒) 标记，具体取决于 `showRooIgnoredFiles` 设置（默认为 `true`）。
*   **忽略消息**：单文件引用返回 "(File is ignored by .rooignore)" 而非内容。
*   **错误消息**：如果工具操作被阻止，Roo 会收到错误：`"Access to [file_path] is blocked by the .rooignore file settings. You must try to continue in the task without using this file, or ask the user to update the .rooignore file."`
*   **聊天通知**：当操作因 `.rooignore` 被阻止时，你通常会在 Roo 聊天界面中看到通知。

本指南帮助你了解 `.rooignore` 功能、其能力和当前限制，以便你有效管理 Roo 与代码库的交互。