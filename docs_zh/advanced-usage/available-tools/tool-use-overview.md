---
description: Roo Code 工具系统的综合指南，包括工具组、调用机制、模式集成和 AI 开发最佳实践。
keywords:
  - Roo Code 工具
  - 工具系统
  - 工具组
  - AI 开发
  - 工具架构
  - 模式集成
  - 工具安全
  - 工作流工具
  - VS Code AI
image: /img/social-share.jpg
---

# 工具使用概述

Roo Code 实现了一个复杂的工具系统，允许 AI 模型以受控和安全的方式与您的开发环境交互。本文档解释了工具的工作原理、调用时机以及管理方式。

---

## 核心概念

### 工具组

工具根据其功能组织成逻辑组：

| 类别 | 目的 | 工具 | 常见用途 |
|----------|---------|-------|------------|
| **读取组** | 文件系统读取和探索 | [read_file](/advanced-usage/available-tools/read-file), [list_files](/advanced-usage/available-tools/list-files), [list_code_definition_names](/advanced-usage/available-tools/list-code-definition-names) | 代码探索和分析 |
| **搜索组** | 模式和语义搜索 | [search_files](/advanced-usage/available-tools/search-files), [codebase_search](/advanced-usage/available-tools/codebase-search) | 查找代码模式和功能 |
| **编辑组** | 文件系统修改 | [apply_diff](/advanced-usage/available-tools/apply-diff), [write_to_file](/advanced-usage/available-tools/write-to-file) | 代码更改和文件操作 |
| **浏览器组** | Web 自动化 | [browser_action](/advanced-usage/available-tools/browser-action) | Web 测试和交互 |
| **命令组** | 系统命令执行 | [execute_command](/advanced-usage/available-tools/execute-command), [run_slash_command](/advanced-usage/available-tools/run-slash-command)* | 运行脚本、构建项目、执行命令模板 |
| **MCP 组** | 外部工具集成 | [use_mcp_tool](/advanced-usage/available-tools/use-mcp-tool), [access_mcp_resource](/advanced-usage/available-tools/access-mcp-resource) | 通过外部服务器的专用功能 |
| **工作流组** | 模式和任务管理 | [switch_mode](/advanced-usage/available-tools/switch-mode), [new_task](/advanced-usage/available-tools/new-task), [ask_followup_question](/advanced-usage/available-tools/ask-followup-question), [attempt_completion](/advanced-usage/available-tools/attempt-completion) | 上下文切换和任务组织 |

*_实验性功能 - 需要在设置中明确启用_

### 始终可用的工具

某些工具在任何模式下都可访问：

- [ask_followup_question](/advanced-usage/available-tools/ask-followup-question)：从用户收集附加信息
- [attempt_completion](/advanced-usage/available-tools/attempt-completion)：发出任务完成信号
- [switch_mode](/advanced-usage/available-tools/switch-mode)：更改操作模式
- [new_task](/advanced-usage/available-tools/new-task)：创建子任务

---

## 可用工具

### 读取工具
这些工具帮助 Roo 理解您的代码和项目：

- [read_file](/advanced-usage/available-tools/read-file) - 检查文件内容
- [list_files](/advanced-usage/available-tools/list-files) - 映射项目的文件结构
- [list_code_definition_names](/advanced-usage/available-tools/list-code-definition-names) - 创建代码的结构映射

### 搜索工具
这些工具帮助 Roo 在代码库中查找模式和功能：

- [search_files](/advanced-usage/available-tools/search-files) - 使用正则表达式在多个文件中查找模式
- [codebase_search](/advanced-usage/available-tools/codebase-search) - 在索引的代码库上执行语义搜索

### 编辑工具
这些工具帮助 Roo 对代码进行更改：

- [apply_diff](/advanced-usage/available-tools/apply-diff) - 对代码进行精确、微创的更改
- [write_to_file](/advanced-usage/available-tools/write-to-file) - 创建新文件或完全重写现有文件

### 浏览器工具
这些工具帮助 Roo 与 Web 应用交互：

- [browser_action](/advanced-usage/available-tools/browser-action) - 自动化浏览器交互

### 命令工具
这些工具帮助 Roo 执行命令：

- [execute_command](/advanced-usage/available-tools/execute-command) - 运行系统命令和程序
- [run_slash_command](/advanced-usage/available-tools/run-slash-command) - 执行预定义的斜杠命令以获得模板化指令 *(实验性 - 需要启用)*

### MCP 工具
这些工具帮助 Roo 连接到外部服务：

- [use_mcp_tool](/advanced-usage/available-tools/use-mcp-tool) - 使用专用的外部工具
- [access_mcp_resource](/advanced-usage/available-tools/access-mcp-resource) - 访问外部数据源

### 工作流工具
这些工具帮助管理工作流和任务流：

- [ask_followup_question](/advanced-usage/available-tools/ask-followup-question) - 从您那里获取附加信息
- [attempt_completion](/advanced-usage/available-tools/attempt-completion) - 呈现最终结果
- [switch_mode](/advanced-usage/available-tools/switch-mode) - 切换到不同的模式以执行专用任务
- [new_task](/advanced-usage/available-tools/new-task) - 创建新子任务

---

## 工具调用机制

### 处理复杂任务

对于需要多个步骤的某些复杂操作，Roo 不会临时决定。相反，它遵循预定义的内部计划以确保一致性和准确性。

一个典型的例子是创建新的 MCP 服务器，内部标识为 `create_mcp_server`。**此标识不代表您会看到被调用的工具。** 相反，当您要求 Roo 创建服务器时，它会触发此已知的多步骤工作流。

当您要求 Roo 创建服务器时，此特定工作流由 Roo 使用其内部 `fetch_instructions` 工具（任务 `create_mcp_server`）启动，以检索详细计划。然后此计划指导 Roo 按顺序调用几个标准、记录的工具，例如：

*   [`execute_command`](/advanced-usage/available-tools/execute-command) 用于运行设置脚本（例如，`npx @modelcontextprotocol/create-server`）。
*   [`write_to_file`](/advanced-usage/available-tools/write-to-file) 或 [`apply_diff`](/advanced-usage/available-tools/apply-diff) 用于创建或修改服务器代码和配置文件。
*   [`ask_followup_question`](/advanced-usage/available-tools/ask-followup-question) 从您那里收集必要的信息，如 API 密钥。
*   其他标准工具，根据需要用于确定文件位置或更新配置条目等步骤。

因此，虽然整体任务（如 `create_mcp_server`）很复杂，但它最终是通过智能编排您环境中可用的标准工具来完成的。这种方法使 Roo 能够通过利用此处记录的工具可靠地执行复杂操作。

### 调用工具的时机

工具在特定条件下被调用：

1. **直接任务需求**
   - 当 LLM 需要特定操作来完成任务时
   - 作为用户请求的响应
   - 在自动化工作流期间

2. **基于模式的可用性**
   - 不同模式启用不同的工具集
   - 模式切换可能触发工具可用性变化
   - 某些工具仅限于特定模式

3. **上下文相关调用**
   - 基于工作区的当前状态
   - 作为系统事件的响应
   - 在错误处理和恢复期间

### 决策过程

系统使用多步骤过程确定工具可用性：

1. **模式验证**
   ```typescript
   isToolAllowedForMode(
       tool: string,
       modeSlug: string,
       customModes: ModeConfig[],
       toolRequirements?: Record<string, boolean>,
       toolParams?: Record<string, any>
   )
   ```

2. **需求检查**
   - 系统能力验证
   - 资源可用性
   - 权限验证

3. **参数验证**
   - 所需参数的存在
   - 参数类型检查
   - 值验证

---

## 技术实现

### 工具调用处理

1. **初始化**
   - 验证工具名称和参数
   - 检查模式兼容性
   - 验证需求

2. **执行**
   ```typescript
   const toolCall = {
       type: "tool_call",
       name: chunk.name,
       arguments: chunk.input,
       callId: chunk.callId
   }
   ```

3. **结果处理**
   - 成功/失败确定
   - 结果格式化
   - 错误处理

### 安全和权限

1. **访问控制**
   - 文件系统限制
   - 命令执行限制
   - 网络访问控制

2. **验证层**
   - 工具特定验证
   - 基于模式的限制
   - 系统级检查

---

## 模式集成

### 基于模式的工具访问

工具根据当前模式提供：

- **代码模式**：完全访问文件系统工具、代码编辑功能、命令执行
- **询问模式**：仅限于读取工具、信息收集能力，无文件系统修改
- **架构模式**：以设计为重点的工具、文档功能、有限的执行权限
- **自定义模式**：可配置特定工具访问以用于专用工作流

### 模式切换

1. **过程**
   - 当前模式状态保存
   - 工具可用性更新
   - 上下文切换

2. **对工具的影响**
   - 工具集变化
   - 权限调整
   - 上下文保持

---

## 最佳实践

### 工具使用指南

1. **效率**
   - 为任务使用最具体的工具
   - 避免冗余的工具调用
   - 可能时批量操作

2. **安全**
   - 在工具调用前验证输入
   - 使用最小必需权限
   - 遵循安全最佳实践

3. **错误处理**
   - 实现适当的错误检查
   - 提供有意义的错误消息
   - 优雅地处理故障

### 常见模式

1. **信息收集**
   ```
   [ask_followup_question](/advanced-usage/available-tools/ask-followup-question) → [read_file](/advanced-usage/available-tools/read-file) → [codebase_search](/advanced-usage/available-tools/codebase-search)
   ```

2. **代码修改**
   ```
   [read_file](/advanced-usage/available-tools/read-file) → [apply_diff](/advanced-usage/available-tools/apply-diff) → [attempt_completion](/advanced-usage/available-tools/attempt-completion)
   ```

3. **任务管理**
   ```
   [new_task](/advanced-usage/available-tools/new-task) → [switch_mode](/advanced-usage/available-tools/switch-mode) → [execute_command](/advanced-usage/available-tools/execute-command)
   ```

---

## 错误处理和恢复

### 错误类型

1. **工具特定错误**
   - 参数验证失败
   - 执行错误
   - 资源访问问题

2. **系统错误**
   - 权限被拒绝
   - 资源不可用
   - 网络故障

3. **上下文错误**
   - 工具的无效模式
   - 缺少需求
   - 状态不一致

### 恢复策略

1. **自动恢复**
   - 重试机制
   - 后备选项
   - 状态恢复

2. **用户干预**
   - 错误通知
   - 恢复建议
   - 手动干预选项