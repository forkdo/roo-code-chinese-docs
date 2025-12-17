---
description: 了解 Roo Code 如何使用工具与您的系统交互。理解文件操作、命令执行、浏览器控制和审批工作流程。
keywords:
  - Roo Code 工具
  - AI 工具
  - 文件操作
  - 命令执行
  - 浏览器自动化
  - 工具审批
image: /img/social-share.jpg
---

# 工具的工作原理

Roo Code 使用工具与您的代码和环境进行交互。这些专用助手执行特定操作，例如读取文件、编辑代码、运行命令或搜索代码库。工具为常见开发任务提供自动化支持，无需手动执行。

---

## 工具工作流程

用自然语言描述您想要完成的任务，Roo Code 将：

1. 根据您的请求选择合适的工具
2. 向您展示工具及其参数以供审核
3. 执行已批准的工具并向您展示结果
4. 继续此流程直到任务完成

---

## 工具分类

| 分类 | 用途 | 工具名称 |
| :------- | :------ | :--------- |
| 读取 | 访问文件内容和代码结构 | `read_file`, `search_files`, `list_files`, `list_code_definition_names` |
| 编辑 | 创建或修改文件和代码 | `write_to_file`, `apply_diff` |
| 执行 | 运行命令和执行系统操作 | `execute_command` |
| 浏览器 | 与网页内容交互 | `browser_action` |
| 工作流 | 管理任务流程和上下文 | `ask_followup_question`, `attempt_completion`, `switch_mode`, `new_task` |

---

## 示例：使用工具

以下是典型工具交互的工作方式：

<img src="/img/how-tools-work/how-tools-work.png" alt="工具审批界面显示保存和拒绝按钮，以及自动批准复选框" width="600" />

*工具审批界面显示保存/拒绝按钮和自动批准选项。*

**用户：** 创建一个名为 `greeting.js` 的文件，记录问候消息

**Roo Code：** （如上图所示，提议使用 `write_to_file` 工具）
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

**用户：** （点击界面上的“保存”按钮）

**Roo Code：** （确认文件创建）

---

## 工具安全和审批

每次使用工具都需要您的明确批准。当 Roo 提议使用工具时，您会看到：

* “保存”按钮用于批准并执行工具
* “拒绝”按钮用于拒绝提议的工具
* 可选的“自动批准”设置，用于受信任的操作

这种安全机制确保您对要修改的文件、执行的命令以及代码库的更改保持控制。在保存之前，请始终仔细审核工具提议。

---

## 核心工具参考

| 工具名称 | 描述 | 分类 |
| :-------- | :---------- | :------- |
| `read_file` | 读取带有行号的文件内容 | 读取 |
| `search_files` | 在文件中搜索文本或正则表达式模式 | 读取 |
| `list_files` | 列出指定位置的文件和目录 | 读取 |
| `list_code_definition_names` | 列出类和函数等代码定义 | 读取 |
| `write_to_file` | 创建新文件或覆盖现有文件 | 编辑 |
| `apply_diff` | 对文件的特定部分进行精确更改 | 编辑 |
| `execute_command` | 在 VS Code 终端中运行命令 | 执行 |
| `browser_action` | 在无头浏览器中执行操作 | 浏览器 |
| `ask_followup_question` | 向您提出澄清问题 | 工作流 |
| `attempt_completion` | 表示任务已完成 | 工作流 |
| `switch_mode` | 切换到不同的操作模式 | 工作流 |
| `new_task` | 使用特定起始模式创建新子任务 | 工作流 |

---

## 了解更多关于工具的信息

有关每个工具的更详细信息，包括完整的参数参考和高级使用模式，请参阅 [工具使用概述](/advanced-usage/available-tools/tool-use-overview) 文档。