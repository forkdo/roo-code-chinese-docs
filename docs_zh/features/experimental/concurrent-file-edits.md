---
sidebar_label: '多文件编辑'
description: '使用 Roo Code 的实验性并发文件编辑功能加速重构和多文件更改。在单个操作中编辑多个文件，支持批量审批。'
keywords:
  - 并发文件编辑
  - 多文件编辑
  - 批量编辑
  - 重构
  - "Roo Code 实验性功能"
  - apply_diff
  - "批量审批"
image: /img/social-share.jpg
---

# 并发文件编辑（又名多文件编辑）

在单个操作中编辑工作区中的多个文件，显著加速重构和多文件更改。

---

## 功能说明

<img src="/img/concurrent-file-edits/concurrent-file-edits-1.png" alt="批量差异审批界面，显示多个文件的更改" width="800" />

并发文件编辑允许 Roo 在单个请求中修改工作区中的多个文件。您无需逐个批准每个文件编辑，而是通过统一的批量审批界面一次性审查和批准所有更改。

---

## 使用原因

**传统方式**：顺序文件编辑，需要单独审批
- 编辑文件 A → 审批
- 编辑文件 B → 审批  
- 编辑文件 C → 审批

**使用并发文件编辑**：所有更改一起呈现
- 审查文件 A、B 和 C 的所有建议更改
- 一次批准即可应用所有更改

这减少了中断，并加速了复杂的任务，例如：
- 跨多个文件重构函数
- 在整个代码库中更新配置值
- 重命名组件及其引用
- 应用一致的格式或样式更改

---

## 如何启用

:::info 实验性功能
多文件编辑是一个实验性功能，必须在设置中启用。

1. 打开 Roo Code 设置（点击 Roo Code 中的齿轮图标）
2. 导航到 **Roo Code > 实验性设置**
3. 启用 **启用多文件编辑** 选项

<img src="/img/concurrent-file-edits/concurrent-file-edits.png" alt="实验性设置中的启用多文件编辑切换开关" width="400" />
:::

---

## 使用方法

启用后，Roo 会在适当时自动使用并发编辑。您将看到一个“批量差异审批”界面，显示：

- 所有要修改的文件
- 每个文件的建议更改
- 批准所有更改或单独审查的选项

### 示例工作流

1. 要求 Roo “更新所有 API 端点以使用新的身份验证方法”
2. Roo 分析您的代码库并识别所有受影响的文件
3. 您收到一个单一的批量审批请求，显示以下文件的更改：
   - `src/api/users.js`
   - `src/api/products.js`
   - `src/api/orders.js`
   - `src/middleware/auth.js`
4. 在统一的差异视图中审查所有更改
5. 批准以同时应用所有更改

---

## 技术详情

此功能利用了 [`apply_diff`](/advanced-usage/available-tools/apply-diff#experimental-multi-file-edits-multi_file_apply_diff) 工具的实验性多文件功能。有关实现、XML 格式以及 `MultiFileSearchReplaceDiffStrategy` 工作原理的详细信息，请参阅 [apply_diff 文档](/advanced-usage/available-tools/apply-diff#experimental-multi-file-edits-multi_file_apply_diff)。

---

## 最佳实践

### 启用时机
- 使用功能强大的 AI 模型（Claude 3.5 Sonnet、GPT-4 等）
- 习惯一次性审查多个更改

### 保持禁用时机
- 使用功能较弱的模型，可能难以处理复杂的多文件上下文
- 偏好单独审查每个更改

---

## 限制

- **实验性**：此功能仍在完善中，可能存在边缘情况
- **依赖模型**：与功能更强大的 AI 模型配合使用效果更佳
- **令牌使用**：由于上下文更大，初始请求可能使用更多令牌
- **复杂性**：非常大的批量操作可能更难审查

---

## 故障排除

### 更改未批量处理
- 确认设置中已启用实验标志
- 检查您的模型是否支持多文件操作
- 确保文件未被 `.rooignore` 限制

### 审批 UI 未出现
- 更新到最新版本的 Roo Code
- 检查 VS Code 的输出面板是否有错误
- 尝试禁用并重新启用该功能

### 性能问题
- 对于非常大的批量操作，考虑将任务分解为较小的块
- 如果使用有限的 API 配额，请监控令牌使用情况

---

## 参阅

- [`apply_diff` 工具文档](/advanced-usage/available-tools/apply-diff) - 详细技术信息
- [实验性功能](/features/experimental/experimental-features) - 其他实验性功能
- [`.rooignore` 配置](/features/rooignore) - 文件访问限制