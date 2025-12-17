---
description: 使用 list_code_definition_names 工具列出类、函数和接口，获取代码库的结构概览。
keywords:
  - list_code_definition_names
  - 代码结构
  - 代码定义
  - Roo Code 工具
  - 代码库概览
  - Tree-sitter
image: /img/social-share.jpg
---

# list_code_definition_names

`list_code_definition_names` 工具通过列出指定目录顶层源文件中的代码定义，为代码库提供结构概览。它通过显示行号和定义片段，帮助 Roo 理解代码架构。

---

## 参数

该工具接受以下参数：

- `path`（必需）：要列出顶层源代码定义的目录路径，相对于当前工作目录

---

## 功能说明

此工具扫描指定目录顶层的源代码文件，提取类、函数和接口等代码定义。它显示每个定义的行号和实际代码，提供一种快速映射代码库重要组件的方法。

---

## 使用场景

- 当 Roo 需要快速理解代码库架构时
- 当 Roo 需要在多个文件中定位重要代码结构时
- 当计划重构或扩展现有代码时
- 在使用其他工具深入实现细节之前
- 在识别代码库不同部分之间的关系时

---

## 主要特性

- 从源文件中提取类、函数、方法、接口等定义
- 显示每个定义的行号和实际源代码
- 支持多种编程语言，包括 JavaScript、TypeScript、Python、Rust、Go、C++、C、C#、Ruby、Java、PHP、Swift 和 Kotlin
- 仅处理指定目录顶层的文件（不包括子目录）
- 最多处理 50 个文件以保证性能
- 专注于顶层定义，避免细节过多
- 帮助识别代码库中的代码组织模式
- 创建代码库架构的心理地图
- 与其他工具（如 `read_file`）配合使用进行深度分析

---

## 局限性

- 仅识别顶层定义，不包括嵌套定义
- 仅处理指定目录顶层的文件，不包括子目录
- 每次请求最多处理 50 个文件
- 依赖于特定语言的解析器，检测质量因语言而异
- 可能无法识别复杂语法语言中的所有定义
- 不能替代阅读代码来理解实现细节
- 无法检测运行时模式或动态代码关系
- 不提供定义使用方式的信息
- 对于高度动态或元编程的代码，准确性可能降低
- 仅限于实现的 Tree-sitter 解析器支持的特定语言

---

## 工作原理

当调用 `list_code_definition_names` 工具时，它遵循以下流程：

1. **参数验证**：验证必需的 `path` 参数
2. **路径解析**：将相对路径解析为绝对路径
3. **目录扫描**：仅扫描指定目录顶层的源代码文件（非递归）
4. **文件过滤**：将处理限制在最多 50 个文件内
5. **语言检测**：根据文件扩展名识别文件类型（.js、.jsx、.ts、.tsx、.py、.rs、.go、.cpp、.hpp、.c、.h、.cs、.rb、.java、.php、.swift、.kt、.kts）
6. **代码解析**：使用 Tree-sitter 解析代码并提取定义，包括以下步骤：
   - 将文件内容解析为抽象语法树（AST）
   - 使用特定语言的查询字符串创建查询
   - 按照在文件中的位置对捕获进行排序
7. **结果格式化**：输出带行号和实际源代码的定义

---

## 输出格式

输出显示文件路径，后跟每个定义的行号和实际源代码。例如：

```
src/utils.js:
0--0 | export class HttpClient {
5--5 | formatDate() {
10--10 | function parseConfig(data) {

src/models/User.js:
0--0 | interface UserProfile {
10--10 | export class User {
20--20 | function createUser(data) {
```

每行显示：
- 定义的起始和结束行号
- 作为分隔符的管道符号（|）
- 定义的实际源代码

这种输出格式帮助您快速查看定义在文件中的位置及其实施细节。

---

## 使用示例

- 开始新任务时，Roo 首先列出关键代码定义以了解项目的整体结构。
- 规划重构工作时，Roo 使用此工具识别可能受影响的类和函数。
- 探索不熟悉的代码库时，Roo 在深入实现细节之前映射重要代码结构。
- 添加新功能时，Roo 识别现有模式和相关代码定义以保持一致性。
- 排查错误时，Roo 映射代码库结构以定位问题的潜在来源。
- 规划架构更改时，Roo 识别跨文件的所有受影响组件。

---

## 使用示例

列出当前目录中的代码定义：
```
<list_code_definition_names>
<path>.</path>
</list_code_definition_names>
```

检查特定模块的结构：
```
<list_code_definition_names>
<path>src/components</path>
</list_code_definition_names>
```

探索实用工具库：
```
<list_code_definition_names>
<path>lib/utils</path>
</list_code_definition_names>
```