---
description: 探索 read_file 工具的功能，包括检查文件内容、支持行范围、PDF/DOCX 提取、图像读取，以及实验性的多文件并发读取。
keywords:
  - read_file
  - Roo Code 工具
  - 文件读取
  - 并发读取
  - 行号
  - PDF 提取
  - DOCX 支持
  - 图像支持
  - OCR 工作流
  - 代码分析
  - VS Code AI
image: /img/social-share.jpg
---

# read_file

`read_file` 工具用于检查项目中的文件内容。它允许 Roo 理解代码、配置文件、文档，以及现在的图像，从而提供更好的帮助。

:::info 多文件支持
`read_file` 工具通过 `args` 格式接受多个文件。并发性和每请求限制在 UI 中配置；后端工具不会硬性强制执行文件数量上限。某些模型可能使用简化的单文件变体。

**注意：** 在读取文件时（即使是单个文件），LLM 会看到一条消息，鼓励多文件读取：“同时读取多个文件对 LLM 更高效。如果当前任务涉及其他文件，请同时读取它们。”
:::

---

## 参数

该工具接受两种格式的参数，具体取决于您的配置：

### 标准格式（单文件）

- `path`（必需）：相对于当前工作目录的文件路径
- `start_line`（可选）：开始读取的行号（1 基索引）
- `end_line`（可选）：结束读取的行号（1 基，包含）

:::note 遗留格式
虽然单文件参数（`path`、`start_line`、`end_line`）仍受向后兼容性支持，但我们建议使用较新的 `args` 格式以保持一致性和未来兼容性。
:::

### 增强格式（多文件）

该工具还接受包含多个文件规范的 `args` 参数。并发性在 UI 中配置；后端接受多个文件，无论该设置如何。某些模型可能使用简单的单文件工具。

- `args`（必需）：包含多个文件规范的容器
  - `file`（必需）：单个文件规范
    - `path`（必需）：文件路径
    - `line_range`（可选）：行范围规范（例如 "1-50" 或 "100-150"）。每个文件可以指定多个 `line_range` 元素。

---

## 功能说明

此工具读取指定文件的内容并返回带行号的文本，便于引用。它可以读取整个文件或特定部分，从 PDF 和 Word 文档中提取文本，并显示各种格式的图像。

---

## 使用场景

- 当 Roo 需要理解现有代码结构时
- 当 Roo 需要分析配置文件时
- 当 Roo 需要从文本文件中提取信息时
- 当 Roo 需要在建议更改前查看代码时
- 当需要引用特定行号进行讨论时

---

## 主要特性

- 显示带行号的文件内容，便于引用
- 通过指定行范围读取文件的特定部分
- 从 PDF、DOCX、XLSX 和 IPYNB 文件中提取可读文本
- **图像支持**：以多种格式显示图像（PNG、JPG、JPEG、GIF、WebP、SVG、BMP、ICO、TIFF/TIF、AVIF）
- **智能读取**：感知令牌预算的读取，自动截断以适应剩余预算，而不是失败
- **大文件预览**：对于非常大的文件返回 100KB 预览，便于快速检查
- **优雅的错误恢复**：从流错误中恢复，并引导您使用 `line_range` 进行有针对性的读取
- 当未指定行范围时，自动截断大文本文件，显示文件开头
- 当内容因行限制被截断时，附加 `list_code_definition_names` 以提供代码结构概览
- 高效流式传输仅请求的行范围以提高性能
- 便于使用行号讨论代码的特定部分
- **多文件支持**：通过批量批准同时读取多个文件

---

## 多文件功能

支持多文件读取。并发性和每请求限制在设置中配置；后端工具不会硬性强制执行文件数量上限，行为可能受模型/工具选择的限制：

### 配置
- **位置**：设置 > 上下文 > "并发文件读取限制"
- **描述**："read_file 工具可以并发处理的最大文件数。较高的值可能加速读取多个小文件，但会增加内存使用。"
- **范围**：1-100（滑块控制）
- **默认值**：5

### 批处理
- UI 可配置限制，每请求最多 100 个文件（默认 5）。后端不会硬性强制执行上限；实际行为可能受模型/工具限制。
- 并行处理以提高性能
- 批量批准界面用于用户同意

### 改进的用户体验
- 多个文件的单个批准对话框
- 单个文件覆盖选项
- 清晰显示将访问哪些文件
- 优雅处理混合成功/失败场景

### 提高效率
- 减少多次批准对话框的中断
- 通过并行文件读取加快处理速度
- 相关文件的智能批处理
- 可配置的并发限制以匹配系统能力

---

## 限制

- **大文件**：对于极大的文件，工具可能返回预览，并引导您使用 `line_range` 进行有针对性的读取。
- **二进制文件**：除了 PDF、DOCX、XLSX、IPYNB 和支持的图像格式外，内容可能不可读。
- **UI/模型约束**：并发限制和每请求文件计数在 UI 中配置；后端工具不会硬性强制执行上限。
- **图像文件**：图像以 base64 数据 URL 形式提供。高分辨率图像可能很大。
  - 默认单图像最大大小：5MB
  - 默认总图像最大大小：20MB
- **不支持的二进制格式**：返回 `<binary_file format="ext">Binary file - content not displayed</binary_file>` 占位符。
- **令牌预算**：内容可能因适应剩余令牌预算而被截断；通知会指示如何继续。

---

## 工作原理

调用 `read_file` 工具时，它遵循以下过程：

1. **参数验证**：验证必需的 `path` 参数和可选参数
2. **路径解析**：将相对路径解析为绝对路径
3. **读取策略选择**：
   - 工具使用严格的优先级层次（下文详述）
   - 它在范围读取、自动截断或全文件读取之间选择
4. **内容处理**：
   - 为内容添加行号（例如 "1 | const x = 13"，其中 "1 |" 是行号）
   - 对于截断的文件，添加截断通知和方法定义
   - 对于特殊格式（PDF、DOCX、XLSX、IPYNB），提取可读文本
   - 对于图像格式，XML 包含带大小的 `<notice>`；实际图像作为 base64 数据 URL 附加到工具结果中（不返回尺寸；MIME 类型由数据 URL 暗示）

---

## 读取策略优先级

工具使用清晰的决策层次来确定如何读取文件：

1. **第一优先级：显式行范围**
   - 遗留单文件格式：必须同时提供 `start_line` 和 `end_line` 才能进行范围读取；否则正常读取。
   - 多文件 `args` 格式：每个文件指定一个或多个 `line_range` 条目。
   - 范围读取仅流式传输请求的行，绕过 `maxReadFileLine`，优先于其他选项。

2. **第二优先级：令牌预算管理**
   - 工具遵守剩余令牌预算以防止上下文溢出
   - 如果文件超过剩余预算，它会自动截断以适应
   - 对于非常大的文件（超过实际限制），返回 100KB 预览以快速检查
   - 提供使用 `line_range` 进行有针对性读取的指导
   - 优雅地从流错误中恢复，并建议替代方法

3. **第三优先级：大文本文件的自动截断**
   - 仅在以下所有条件为真时应用：
     - 未指定 `start_line` 或 `end_line`。
     - 文件被识别为基于文本的文件（不是 PDF/DOCX/XLSX/IPYNB 等二进制文件）。
     - 文件的总行数超过 `maxReadFileLine` 设置（可配置；UI 默认值可能为 500；后端在未设置时使用 `-1`——无行限制）。
   - 当自动截断发生时：
     - 工具仅读取前 `maxReadFileLine` 行。
     - 它附加通知，如：`仅显示 X 行（共 Y 行）。如果需要读取更多行，请使用 line_range。`
     - 对于代码文件，它附加 `list_code_definition_names` 以提供结构概览。
   - **特殊情况——仅定义模式**：当 `maxReadFileLine` 设置为 `0` 时，工具仅返回代码定义而不返回文件内容（加上通知）。

4. **默认行为：读取整个文件**
    - 如果既未给出显式范围，也未应用自动截断（例如，文件在行限制内，或者是支持的二进制类型），工具读取整个内容。
    - 对于 PDF 和 DOCX 等支持的格式，它尝试提取完整文本内容。
    - 对于图像格式，它返回可以在聊天界面中显示的 base64 编码数据 URL。

---

## 使用示例

以下是演示 `read_file` 工具使用方法和您可能收到的典型输出的几个场景。

### 读取整个文件

读取文件的完整内容：

**输入：**
```xml
<read_file>
<path>src/app.js</path>
</read_file>
```

**模拟输出（对于小文件如 `example_small.txt`）：**
```
1 | This is the first line.
2 | This is the second line.
3 | This is the third line.
```
*(输出根据实际文件内容而变化)*

### 读取特定行

仅读取特定行范围（例如 46-68）：

**输入：**
```xml
<read_file>
<path>src/app.js</path>
<start_line>46</start_line>
<end_line>68</end_line>
</read_file>
```

**模拟输出（对于 `example_five_lines.txt` 的第 2-3 行）：**
```
2 | Content of line two.
3 | Content of line three.
```
*(输出仅显示请求的行及其原始行号)*

### 读取大文本文件（自动截断）

读取大文本文件且未指定行范围时，如果文件超过内部行限制（例如 500 行），工具会自动截断内容。

**输入：**
```xml
<read_file>
<path>logs/large_app.log</path>
</read_file>
```

**模拟输出（对于 1500 行日志文件，限制为 500 行）：**
```
1 | Log entry 1...
2 | Log entry 2...
...
500 | Log entry 500...

仅显示 500 行（共 1500 行）。使用 line_range 读取特定部分。
// 可选：代码文件可能在此处显示源代码定义摘要
```
*(输出显示开头行，直到 `maxReadFileLine` 限制，加上截断通知。使用行范围进行完整访问。)*

### 仅读取定义

当用户设置中 `maxReadFileLine` 设置为 `0` 时，工具仅返回源代码定义而不返回文件内容：

**输入：**
```xml
<!-- 假设用户设置中 maxReadFileLine 设置为 0 -->
<read_file>
<path>src/services/auth.service.ts</path>
</read_file>
```

**模拟输出：**
```xml
<file>
  <path>src/services/auth.service.ts</path>
  <list_code_definition_names>
    class AuthService
      method validateUser
      method generateToken
  </list_code_definition_names>
  <notice>仅显示 0 行（共 150 行）。如果需要读取更多行，请使用 line_range</notice>
</file>
```
*(此模式提供文件结构的快速概览而不读取内容。)*

### 尝试读取不存在的文件

如果指定的文件不存在：

**输入：**
```xml
<read_file>
<path>non_existent_file.txt</path>
</read_file>
```

**模拟输出（错误）：**
```
Error: File not found at path 'non_existent_file.txt'.
```

### 尝试读取被阻止的文件

如果文件被 `.rooignore` 文件中的规则排除：

**输入：**
```xml
<read_file>
<path>.env</path>
</read_file>
```

**模拟输出（错误）：**
```xml
<file>
  <path>.env</path>
  <error>Access denied by .rooignore rules</error>
</file>
```

---

### 使用令牌预算管理的智能读取

读取大文件时，工具自动管理令牌预算以防止上下文溢出。

**场景：** 未指定行范围时读取非常大的文件。

**输入：**
```xml
<read_file>
<path>logs/massive-debug.log</path>
</read_file>
```

**模拟输出（对于超过令牌预算的文件）：**
```
预览：显示文件的前 …MB（共 …MB）。使用 line_range 读取特定部分。
```

替代截断通知：
```
文件因上下文限制被截断为 N 行（共 M 行）。使用 line_range 读取特定部分。
```

此行为确保：
- 小文件完全读取，无开销
- 大文件自动截断以适应剩余令牌预算
- 非常大的文件提供快速预览
- 您收到使用 `line_range` 进行有针对性读取的指导
- 流错误得到优雅处理

**使用 line_range 进行有针对性读取的示例：**
```xml
<read_file>
<path>logs/massive-debug.log</path>
<start_line>1000</start_line>
<end_line>1100</end_line>
</read_file>
```

## 图像读取示例

`read_file` 工具现在支持直接在聊天界面中读取和显示图像。这实现了强大的视觉分析工作流。

### 读取单个图像

**输入：**
```xml
<read_file>
<path>assets/logo.png</path>
</read_file>
```

**输出：**
```xml
<file>
  <path>assets/logo.png</path>
  <notice>Image file (123 KB)</notice>
</file>
```

图像以内联方式显示在聊天中（base64 数据 URL 附加到工具结果）。不返回尺寸；MIME 类型由数据 URL 暗示。

### OCR 工作流示例

从文件夹中读取多个图像以提取文本：

**输入：**
```xml
<read_file>
<args>
  <file>
    <path>screenshots/page1.png</path>
  </file>
  <file>
    <path>screenshots/page2.png</path>
  </file>
  <file>
    <path>screenshots/page3.png</path>
  </file>
</args>
</read_file>
```

**用法：**
```
请从这些截图图像中提取所有文本，并将它们编译成单个 markdown 文档。
```

### 设计审查工作流

分析多个设计草图：

**输入：**
```xml
<read_file>
<args>
  <file>
    <path>designs/homepage-v1.jpg</path>
  </file>
  <file>
    <path>designs/homepage-v2.jpg</path>
  </file>
  <file>
    <path>designs/mobile-view.png</path>
  </file>
</args>
</read_file>
```

**用法：**
```
比较这些设计草图并提供以下方面的反馈：
1. 视觉一致性
2. 移动响应性
3. 可访问性问题
4. UI/UX 改进
```

### 支持的图像格式

该工具支持以下图像格式：
- PNG
- JPG/JPEG
- GIF
- WebP
- SVG
- BMP
- ICO
- TIFF/TIF
- AVIF

### 图像分析用例

1. **文档截图**：从 UI 截图中提取文本并创建文档
2. **错误调试**：分析错误截图以理解问题
3. **设计审查**：比较草图并提供视觉反馈
4. **图表分析**：理解架构图和流程图
5. **代码截图**：当文本不可用时从图像中提取代码
6. **UI 测试**：验证视觉元素和布局

---

## 多文件示例

您可以使用增强的 XML 格式同时读取多个文件。

### 读取多个完整文件

同时读取多个完整文件：

**输入：**
```xml
<read_file>
<args>
  <file>
    <path>src/app.ts</path>
  </file>
  <file>
    <path>src/utils.ts</path>
  </file>
  <file>
    <path>src/config.json</path>
  </file>
</args>
</read_file>
```

**模拟输出：**
```xml
<files>
  <file>
    <path>src/app.ts</path>
    <content>
      1 | import React from 'react'
      2 | import { Utils } from './utils'
      3 | // ... rest of file content
    </content>
  </file>
  <file>
    <path>src/utils.ts</path>
    <content>
      1 | export class Utils {
      2 |   static formatDate