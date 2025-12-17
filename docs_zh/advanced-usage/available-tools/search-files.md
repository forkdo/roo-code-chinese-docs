---
description: 了解 search_files 如何使用正则表达式在代码库中执行强大的搜索，通过 Ripgrep 实现高性能结果。
keywords:
  - search_files
  - Roo Code tools
  - regex search
  - code patterns
  - Ripgrep
  - multi-file search
  - codebase search
  - pattern matching
  - VS Code AI
image: /img/social-share.jpg
---

# search_files

`search_files` 工具在项目工作区内的多个文件中执行正则表达式搜索。出于安全考虑，它无法搜索当前工作区目录之外的内容。它帮助 Roo 在代码库中定位特定的代码模式、文本或其他内容，并提供上下文结果。

---

## 参数

该工具接受以下参数：

- `path`（必需）：要搜索的目录路径，相对于当前工作区目录。搜索被限制在工作区内。
- `regex`（必需）：要搜索的正则表达式模式（使用 Rust 正则表达式语法）
- `file_pattern`（可选）：用于过滤文件的 glob 模式（例如 '*.ts' 用于 TypeScript 文件）
- `respect_gitignore`（可选）：是否遵循 `.gitignore` 模式（默认值：`true`）。设置为 `false` 以搜索所有文件，包括 `.gitignore` 中的文件。

---

## 功能

此工具使用正则表达式在指定目录的文件中搜索，显示每个匹配项及其周围的上下文。它就像一个强大的“在文件中查找”功能，可以在整个项目结构中工作。

---

## 使用场景

- 当 Roo 需要找到特定函数或变量的使用位置时
- 当 Roo 协助重构并需要了解使用模式时
- 当 Roo 需要在多个文件中定位特定代码模式时
- 当 Roo 需要跨多个文件搜索文本并具备过滤能力时

---

## 主要特性

- 在单次操作中跨多个文件搜索，使用高性能 Ripgrep
- **遵循 .gitignore**：自动排除 `.gitignore` 中列出的文件和目录（包括嵌套的 `.gitignore` 文件）
- 显示每个匹配项周围的上下文（前后各 1 行）
- 使用 glob 模式按文件类型过滤（例如仅 TypeScript 文件）
- 提供行号以便轻松引用
- 使用强大的正则表达式模式进行精确搜索
- 自动将结果限制为最多 300 个匹配项并显示通知
- 将超过 500 个字符的行截断，并添加 "[truncated...]" 标记
- 智能地将附近的匹配项合并为单个块以提高可读性

---

## 限制

- 在基于文本的文件上效果最佳（对图像等二进制文件无效）
- 在极大型代码库上性能可能变慢
- 使用 Rust 正则表达式语法，可能与其他正则表达式实现略有不同
- 无法搜索压缩文件或归档文件
- 默认上下文大小是固定的（前后各 1 行）
- 当匹配项彼此接近时，可能显示不同大小的上下文，这是由于结果分组造成的
- 出于安全考虑，搜索严格限制在当前工作区内，无法访问父目录或文件系统上的其他位置
- **默认遵循 .gitignore**：除非使用 `respect_gitignore: false` 明确覆盖，否则 `.gitignore` 中列出的文件将从搜索中排除

---

## 工作原理

当调用 `search_files` 工具时，它遵循以下过程：

1. **参数验证**：验证必需的 `path` 和 `regex` 参数
2. **路径解析**：将相对路径解析为绝对路径
3. **搜索执行**：
   - 使用 Ripgrep (rg) 进行高性能文本搜索
   - 应用文件模式过滤（如果指定）
   - 收集带有周围上下文的匹配项
4. **结果格式化**：
   - 使用文件路径、行号和上下文格式化结果
   - 显示每个匹配项前后各 1 行的上下文
   - 结构化输出以便于阅读
   - 将结果限制为最多 300 个匹配项并显示通知
   - 截断超过 500 个字符的行
   - 将附近的匹配项合并为连续块

---

## 搜索结果格式

搜索结果包括：

- 每个匹配文件的相对路径（以 # 为前缀）
- 每个匹配项前后的上下文行（默认为 1 行）
- 用 3 个空格填充的行号，后跟 ` | ` 和行内容
- 每个匹配组后用分隔线（----）

结果格式示例：
```
# rel/path/to/app.ts
 11 |   // Some processing logic here
 12 |   // TODO: Implement error handling
 13 |   return processedData;
----

# Showing first 300 of 300+ results. Use a more specific search if necessary.
```

当匹配项彼此接近时，它们会被合并为单个块，而不是显示为单独的结果：

```
# rel/path/to/auth.ts
 13 | // Some code here
 14 | // TODO: Add proper validation
 15 | function validateUser(credentials) {
 16 |   // TODO: Implement rate limiting
 17 |   return checkDatabase(credentials);
----
```

---

## 使用示例

当被要求重构函数时，Roo 首先搜索该函数的所有使用位置，以确保全面更改。
当调查错误时，Roo 在整个代码库中搜索类似模式以识别相关问题。
当处理技术债务时，Roo 定位项目中所有的 TODO 注释。
当分析依赖关系时，Roo 查找特定模块的所有导入。

---

## 使用示例

在所有 JavaScript 文件中搜索 TODO 注释：
```
<search_files>
<path>src</path>
<regex>TODO|FIXME</regex>
<file_pattern>*.js</file_pattern>
</search_files>
```

查找特定函数的所有用法：
```
<search_files>
<path>.</path>
<regex>function\s+calculateTotal</regex>
<file_pattern>*.{js,ts}</file_pattern>
</search_files>
```

在整个项目中搜索特定的导入模式：
```xml
<search_files>
<path>.</path>
<regex>import\s+.*\s+from\s+['"]@components/</regex>
</search_files>
```
## 遵循 .gitignore

默认情况下，`search_files` 遵循工作区中的 `.gitignore` 模式，包括嵌套的 `.gitignore` 文件。这可以防止在 `node_modules/`、`dist/` 或其他被忽略的路径中进行搜索。

### 默认行为（遵循 .gitignore）

**输入：**
```xml
<search_files>
<path>.</path>
<regex>TODO</regex>
</search_files>
```

此搜索将**排除** `.gitignore` 中列出的文件和目录，确保在受跟踪的代码上获得集中的结果。

### 覆盖 .gitignore（搜索所有文件）

要搜索**所有文件**，包括 `.gitignore` 中的文件，请明确将 `respect_gitignore` 设置为 `false`：

**输入：**
```xml
<search_files>
<path>.</path>
<regex>TODO</regex>
<respect_gitignore>false</respect_gitignore>
</search_files>
```

这将搜索**所有内容**，包括 `node_modules/`、构建产物和其他被忽略的路径。

**何时覆盖：**
- 调试依赖项或构建输出中的问题
- 搜索生成的代码
- 需要检查所有文件的全面审计
- 调查被忽略的配置文件

---
