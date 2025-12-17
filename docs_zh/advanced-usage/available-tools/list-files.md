---
description: 了解 list_files 工具如何帮助 Roo Code 探索项目结构、列出目录，并通过递归和过滤功能在代码库中导航。
keywords:
  - list_files
  - Roo Code 工具
  - 目录列表
  - 文件探索
  - 项目结构
  - 递归列表
  - 代码库导航
  - VS Code AI
image: /img/social-share.jpg
---

# list_files

`list_files` 工具用于显示指定位置中的文件和目录。它帮助 Roo 理解你的项目结构，并有效地在你的代码库中导航。

---

## 参数

该工具接受以下参数：

- `path`（必需）：要列出内容的目录路径，相对于当前工作目录
- `recursive`（可选）：是否递归列出。使用 `true` 进行递归列表，`false` 或省略则仅列出顶层。

---

## 功能说明

此工具列出指定位置中的所有文件和目录，提供你项目结构的清晰概览。它可以仅显示顶层内容，或递归探索子目录。

---

## 何时使用

- 当 Roo 需要理解你的项目结构时
- 当 Roo 在读取特定文件之前需要探索可用的文件时
- 当 Roo 绘制代码库地图以更好地理解其组织结构时
- 在使用更精确的工具（如 `read_file` 或 `search_files`）之前
- 当 Roo 需要跨项目检查特定文件类型（如配置文件）时

---

## 主要功能

- 列出文件和目录，目录以特殊标记清晰标识
- 提供递归和非递归列表模式
- 在递归模式下智能忽略常见的大目录，如 `node_modules` 和 `.git`
- 在递归模式下遵循 `.gitignore` 规则
- 当启用 `showRooIgnoredFiles` 时，使用锁形符号（🔒）标记被 `.rooignore` 忽略的文件
- 通过利用 `ripgrep` 工具优化文件列表性能
- 对结果进行排序，目录显示在内容之前，保持逻辑层次结构
- 以清晰、有组织的格式呈现结果
- 自动创建你项目结构的心理地图

---

## 限制

- 文件列表默认限制为约 200 个文件，以防止性能问题
- 底层 `ripgrep` 文件列表进程有 10 秒超时限制；如果超时，可能返回部分结果
- 当达到文件限制时，会添加注释，建议在特定子目录上使用 `list_files`
- 不适用于确认你刚刚创建的文件是否存在
- 在非常大的目录结构中可能性能降低
- 出于安全原因，无法列出根目录或主目录中的文件

---

## 工作原理

当调用 `list_files` 工具时，它遵循以下过程：

1. **参数验证**：验证必需的 `path` 参数和可选的 `recursive` 参数
2. **路径解析**：将相对路径解析为绝对路径
3. **安全检查**：防止列出根目录或主目录等敏感位置的文件
4. **目录/文件扫描**：
   - 使用 `ripgrep` 工具高效列出文件，应用 10 秒超时限制
   - 使用 Node.js `fs` 模块列出目录
   - 对递归和非递归模式应用不同的过滤逻辑
5. **结果过滤**：
   - 在递归模式下，跳过 `node_modules`、`.git` 等常见的大目录
   - 在递归模式下遵循 `.gitignore` 规则
   - 处理 `.rooignore` 模式，要么隐藏文件，要么用锁形符号标记
6. **格式化**：
   - 目录用尾部斜杠（`/`）标记
   - 对结果进行排序，目录显示在内容之前，保持逻辑层次结构
   - 当启用 `showRooIgnoredFiles` 时，用锁形符号（🔒）标记被忽略的文件
   - 默认将结果限制为 200 个文件，并添加注释，建议在特定子目录上使用 `list_files`
   - 组织结果以提高可读性

---

## 文件列表格式

文件列表结果包括：

- 每个文件路径在自己的行上显示
- 目录用尾部斜杠（`/`）标记
- 当启用 `showRooIgnoredFiles` 时，被 `.rooignore` 忽略的文件用锁形符号（🔒）标记
- 结果按逻辑排序，目录显示在内容之前
- 当达到文件限制时，会显示消息，建议在特定子目录上使用 `list_files`

示例输出格式：
```
src/
src/components/
src/components/Button.tsx
src/components/Header.tsx
src/utils/
src/utils/helpers.ts
src/index.ts
...
文件列表已截断（显示 200 个中的 543 个文件）。在特定子目录上使用 list_files 以获取更多详细信息。
```

当使用 `.rooignore` 文件且启用 `showRooIgnoredFiles` 时：
```
src/
src/components/
src/components/Button.tsx
src/components/Header.tsx
🔒 src/secrets.json
src/utils/
src/utils/helpers.ts
src/index.ts
```

---

## 使用示例

列出当前目录中的顶层文件：
```
<list_files>
<path>.</path>
</list_files>
```

递归列出源目录中的所有文件：
```
<list_files>
<path>src</path>
<recursive>true</recursive>
</list_files>
```

检查特定的项目子目录：
```
<list_files>
<path>src/components</path>
<recursive>false</recursive>
</list_files>
```