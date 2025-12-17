---
description: 了解 update_todo_list 如何创建具有状态跟踪的动态 TODO 列表，为 Roo Code 中的复杂工作流实现逐步任务管理。
keywords:
  - update_todo_list
  - Roo Code 工具
  - 任务管理
  - TODO 列表
  - 工作流跟踪
  - 清单管理
  - 任务状态
  - 交互式 UI
  - VS Code AI
image: /img/social-share.jpg
---

# update_todo_list

`update_todo_list` 工具可在聊天界面中实现动态、交互式的任务管理。它会用更新后的清单完全替换整个 TODO 列表，确保任务状态始终最新，并为复杂工作流提供逐步跟踪功能。

---

## 参数

该工具接受以下参数：

- `todos`（必需）：表示带有状态指示器的完整清单的 Markdown 格式字符串

---

## 功能说明

此工具创建并管理一个在聊天界面中显示为 UI 组件的交互式待办事项列表。它支持实时任务跟踪、状态更新，以及在复杂工作流执行过程中动态添加新项目。该列表为管理多步骤任务提供了结构化方式，并具有清晰的视觉进度指示器。

---

## 使用场景

- 管理需要结构化跟踪的复杂、多步骤任务时
- Roo 需要显示一系列相关活动的进度时
- 任务需要在继续之前确认每一步的完成情况时
- 在长或复杂工作流中发现新的可执行项目时
- 为用户提供清晰的检查点和进度可见性时

---

## 主要特性

- **完整清单替换**：使用提供的更新版本完全替换现有待办事项列表
- **交互式 UI 组件**：在聊天中显示为可编辑的界面元素
- **多种状态类型**：支持待办、进行中和已完成的任务状态
- **动态任务管理**：在工作流执行过程中实时添加新任务
- **用户友好编辑**：在聊天界面内提供直接编辑功能
- **逐步跟踪**：在更新和继续之前确认每一步
- **进度可视化**：任务完成状态的清晰视觉指示器
- **工作流集成**：与任务执行和完成流程无缝集成

---

## 局限性

- **完全替换**：替换整个列表而不是进行增量更新
- **单层结构**：使用单层 Markdown 清单，不支持嵌套
- **格式要求**：需要特定的 Markdown 复选框语法以正确解析
- **手动更新**：需要显式调用工具来更新列表状态
- **状态管理**：待办事项列表状态与当前任务和对话上下文相关联

---

## 工作原理

调用 `update_todo_list` 工具时，它遵循以下流程：

1. **输入验证**：
   - 验证必需的 `todos` 参数已提供
   - 解析 Markdown 清单格式的语法正确性
   - 检查有效的状态指示器：`[ ]`、`[-]` 和 `[x]`

2. **列表处理**：
   - 处理 Markdown 格式的清单
   - 提取带有状态指示器的各个待办事项
   - 验证每个项目的结构和格式

3. **UI 集成**：
   - 将更新后的待办事项列表呈现给用户以供批准
   - 用新版本替换任何现有的待办事项列表
   - 在聊天界面中将列表渲染为交互式组件

4. **用户交互**：
   - 在编辑模式下允许用户直接在 UI 中编辑待办事项
   - 提供"添加待办事项"功能以实现实时列表扩展
   - 将更改同步回扩展程序以保持状态一致性

5. **状态管理**：
   - 更新任务的内部待办事项列表表示
   - 维护 UI 状态与后端数据之间的同步
   - 在对话交互中保持待办事项列表状态

---

## 清单格式要求

该工具对待办事项使用特定的 Markdown 格式：

### 状态选项
- `[ ]` - 待办任务（未开始）
- `[-]` - 进行中任务（当前正在处理）
- `[x]` - 已完成任务（完全完成）

### 格式规则
- 使用单层 Markdown 清单（不支持嵌套或子任务）
- 按预期执行顺序列出待办事项
- 每个待办事项应清晰且可执行
- 状态应准确反映当前任务状态

---

## 任务管理指南

### 状态更新
- 在所有工作完成后立即标记任务为已完成
- 通过标记下一个任务为进行中来开始新任务
- 对未开始的任务使用待办状态
- 仅在任务完全完成且无未解决依赖项时才标记为已完成

### 动态列表管理
- 在任务执行期间一旦发现新待办事项就立即添加
- 仅在任务不再相关或明确要求时才删除任务
- 保留所有未完成的任务并根据需要更新其状态
- 如果任务被阻塞，保持其为进行中状态，并添加解决步骤的新待办事项

---

## 使用示例

- 开发 Web 应用时，Roo 创建跟踪设计、实现、测试和部署阶段的待办事项列表
- 设置开发环境时，Roo 跟踪依赖项安装、配置步骤和验证任务
- 调试复杂问题时，Roo 维护调查步骤、潜在原因和测试程序的列表
- 重构代码时，Roo 跟踪需要更新的文件、需要修改的测试和需要的文档更改
- 实现新功能时，Roo 管理规划、编码、测试和集成步骤的任务

---

## 使用示例

为开发任务创建初始待办事项列表：
```xml
<update_todo_list>
<todos>
[ ] Analyze requirements
[ ] Design architecture  
[ ] Implement core logic
[ ] Write tests
[ ] Update documentation
</todos>
</update_todo_list>
```

完成第一个任务后更新进度：
```xml
<update_todo_list>
<todos>
[x] Analyze requirements
[-] Design architecture
[ ] Implement core logic
[ ] Write tests
[ ] Update documentation
</todos>
</update_todo_list>
```

添加在实现过程中发现的新任务：
```xml
<update_todo_list>
<todos>
[x] Analyze requirements
[x] Design architecture
[x] Implement core logic
[-] Write tests
[ ] Update documentation
[ ] Add performance benchmarks
[ ] Create deployment script
</todos>
</update_todo_list>
```

管理复杂的调试工作流：
```xml
<update_todo_list>
<todos>
[x] Reproduce the issue
[x] Check recent code changes
[-] Analyze error logs
[ ] Test with different configurations
[ ] Check database queries
[ ] Verify network connectivity
[ ] Create fix and test
</todos>
</update_todo_list>