---
description: 了解 Roo Code 如何使用工具与您的系统进行交互。掌握文件操作、命令执行、浏览器控制以及审批工作流程。
keywords:
  - Roo Code tools
  - AI tools
  - file operations
  - command execution
  - browser automation
  - tool approval
---

# 工具工作原理

Roo Code 使用工具与您的代码和环境进行交互。这些专门的助手程序执行特定操作，例如读取文件、进行编辑、运行命令或搜索代码库。工具为常见开发任务提供自动化功能，无需手动执行。

---

## 工具工作流程

用自然语言描述您想要完成的任务，Roo Code 将：

1. 根据您的请求选择合适的工具
2. 向工具展示其参数供您审核
3. 执行已批准的工具并显示结果
4. 继续此过程，直到您的任务完成

---

## 工具类别

| 类别 | 用途 | 工具名称 |
| :------- | :------ | :--------- |
| 读取 | 访问文件内容和代码结构 | `read_file`、`search_files`、`list_files`、`list_code_definition_names` |
| 编辑 | 创建或修改文件和代码 | `write_to_file`、`apply_diff` |
| 执行 | 运行命令和执行系统操作 | `execute_command` |
| 浏览器 | 与网页内容交互 | `browser_action` |
| 工作流 | 管理任务流程和上下文 | `ask_followup_question`、`attempt_completion`、`switch_mode`、`new_task` |

---

## 示例：使用工具

以下是典型工具交互的工作方式：

<img src="/img/how-tools-work/how-tools-work.png" alt="工具审批界面，显示保存和拒绝按钮以及自动批准复选框" width="600" />

*工具审批界面显示保存/拒绝按钮和自动批准选项。*

**用户：** 创建一个名为 `greeting.js` 的文件，用于记录问候消息

**Roo Code：**（如上图中所示，建议使用 `write_to_file` 工具）
```xml
<write_to_file>
<path>greeting.js</path>
<content>
function greet(name) {
  console.log(`Hello, ${name}!`);
}

greet('World');
</content>
<line_count>5</line_count>
</write_to_file>
```

**用户：**（点击界面中的“保存”按钮）

**Roo Code：**（确认文件创建）

---

## 工具安全性与审批

每次使用工具都需要您的明确批准。当 Roo 建议使用某个工具时，您将看到：

* “保存”按钮，用于批准并执行该工具
* “拒绝”按钮，用于拒绝建议的工具
* 可选的“自动批准”设置，用于可信操作

这种安全机制确保您对哪些文件被修改、执行哪些命令以及代码库如何更改保持控制。在保存工具建议之前，请始终仔细审核。

---

## 核心工具参考

| 工具名称 | 描述 | 类别 |
| :-------- | :---------- | :------- |
| `read_file` | 读取文件内容并显示行号 | 读取 |
| `search_files` | 在文件中搜索文本或正则表达式模式 | 读取 |
| `list_files` | 列出指定位置的文件和目录 | 读取 |
| `list_code_definition_names` | 列出类、函数等代码定义 | 读取 |
| `write_to_file` | 创建新文件或覆盖现有文件 | 编辑 |
| `apply_diff` | 对文件的特定部分进行精确更改 | 编辑 |
| `execute_command` | 在 VS Code 终端中运行命令 | 执行 |
| `browser_action` | 在无头浏览器中执行操作 | 浏览器 |
| `ask_followup_question` | 向您提出澄清问题 | 工作流 |
| `attempt_completion` | 表示任务已完成 | 工作流 |
| `switch_mode` | 切换到不同的操作模式 | 工作流 |
| `new_task` | 创建具有特定起始模式的新子任务 | 工作流 |

---

## 了解更多关于工具的信息

有关每个工具的更多详细信息，包括完整的参数参考和高级使用模式，请参阅[工具使用概览](/advanced-usage/available-tools/tool-use-overview)文档。