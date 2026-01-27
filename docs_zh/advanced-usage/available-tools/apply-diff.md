---
description: 掌握 apply_diff 工具，使用模糊匹配和行提示在 Roo Code 中进行精确的代码更改，并支持多文件操作。
keywords:
  - apply_diff
  - 文件编辑
  - 代码修改
  - 模糊匹配
  - diff 工具
  - Roo Code 工具
  - 多文件编辑
---

# apply_diff

`apply_diff` 工具通过指定要替换的确切内容来对文件进行精确、外科手术式的更改。它使用复杂的策略来查找和应用更改，同时保持正确的代码格式和结构。

---

## 参数

该工具接受以下参数：

- `path`（必需）：相对于当前工作目录的要修改的文件路径。
- `diff`（必需）：使用特定于活动 diff 策略的格式定义更改的搜索/替换块。
- `start_line`（可选）：搜索内容开始位置的提示。_注意：当前主要策略似乎未使用此顶级参数，它依赖于 diff 内容中的 `:start_line:`。_
- `end_line`（可选）：搜索内容结束位置的提示。_注意：当前主要策略似乎未使用此顶级参数。_

---

## 功能说明

此工具使用模糊匹配（由行号提示引导）来精确定位和替换内容，对现有文件应用目标更改。与简单的搜索和替换不同，它根据提供的内容和位置提示识别用于替换的确切块。

---

## 使用时机

- 当 Roo 需要对现有代码进行精确更改而不重写整个文件时。
- 当重构代码的特定部分同时保持周围上下文时。
- 当使用外科手术式的精确度修复现有代码中的错误时。
- 当实现仅修改文件某些部分的功能增强时。

---

## 主要特性

- 使用模糊匹配（标准化字符串上的 Levenshtein 距离）并由 `:start_line:` 提示引导，具有可配置的置信度阈值（通常为 0.8-1.0）。
- 使用 `BUFFER_LINES`（默认 40）提供匹配周围的上下文。
- 在提示的起始行周围的可配置上下文窗口（`bufferLines`）内执行从中间向外的搜索。
- 通过替换确切块被动地保持代码格式和缩进。
- 在应用前以 diff 视图显示更改供用户审查和编辑。
- 跟踪每个文件的连续错误（`consecutiveMistakeCountForApplyDiff`）以防止重复失败。
- 根据 `.rooignore` 规则验证文件访问。
- 有效处理多行编辑。

---

## 局限性

- 最适合具有独特、明显代码部分的情况，以实现可靠识别。
- 在非常大的文件或高度重复的代码模式下性能可能有所不同。
- 如果内容模糊，模糊匹配偶尔可能会选择错误的位置。
- 每种 diff 策略都有特定的格式要求。
- 复杂编辑可能需要仔细的策略选择或手动审查。

---

## 工作原理

当调用 `apply_diff` 工具时，它遵循以下过程：

1.  **参数验证**：验证必需的 `path` 和 `diff` 参数。
2.  **RooIgnore 检查**：验证目标文件路径是否被 `.rooignore` 规则允许。
3.  **文件分析**：加载目标文件内容。
4.  **匹配查找**：使用模糊匹配算法（标准化字符串上的 Levenshtein）并由上下文窗口（`BUFFER_LINES`）内的 `:start_line:` 提示引导，从中间向外搜索以基于置信度阈值定位目标内容。
5.  **更改准备**：通过替换已识别的块生成建议的更改。
6.  **用户交互**：
    *   在 diff 视图中显示更改。
    *   允许用户审查并可能编辑建议的更改。
    *   等待用户批准或拒绝。
7.  **更改应用**：如果获得批准，将更改（可能包括用户编辑）应用到文件。
8.  **错误处理**：如果发生错误（例如，匹配失败、部分应用），会增加文件的 `consecutiveMistakeCountForApplyDiff` 并报告失败类型。
9. **反馈**：返回结果，包括任何用户反馈或错误详情。

---

## Diff 格式要求

`<diff>` 参数需要特定格式，支持单个请求中的一个或多个更改。每个更改块都需要原始内容的行号提示。

*   **要求**：`SEARCH` 块内容的精确匹配（在模糊阈值内），包括空格和缩进。每个块中必须包含 `:start_line:` 数字提示。`:end_line:` 提示是可选的（但解析器支持）。文件内容中的标记如 `<<<<<<<` 必须在 SEARCH 块中转义（`\\`）。

`<diff>` 块的示例格式：

```diff
<<<<<<< SEARCH
:start_line:10
:end_line:12
-------
    // Old calculation logic
    const result = value * 0.9;
    return result;
=======
    // Updated calculation logic with logging
    console.log(`Calculating for value: ${value}`);
    const result = value * 0.95; // Adjusted factor
    return result;
>>>>>>> REPLACE

<<<<<<< SEARCH
:start_line:25
:end_line:25
-------
    const defaultTimeout = 5000;
=======
    const defaultTimeout = 10000; // Increased timeout
>>>>>>> REPLACE
```

---

## 实验性功能：多文件编辑（`MULTI_FILE_APPLY_DIFF`）

`apply_diff` 的实验性版本允许在单个工具调用中对多个文件应用更改。此功能由 `MULTI_FILE_APPLY_DIFF` 实验标志激活。

### 实验模式的主要特性

- **多文件操作**：在单个请求中编辑多个文件，简化复杂的重构任务。
- **批量批准 UI**：当目标为多个文件时，会出现单个 UI 供用户一次性批准或拒绝所有更改，或单独管理每个文件的权限。
- **新 XML 格式**：引入使用 `<args>` 和 `<file>` 标签处理多个操作的更结构化的新 XML 格式。
- **向后兼容**：实验性工具仍与传统的单文件 `path` 和 `diff` 参数格式兼容。

### 工作原理（实验性）

1.  **实验检查**：工具首先检查是否启用了 `MULTI_FILE_APPLY_DIFF` 实验。如果没有，则回退到传统的 `apply_diff` 实现。
2.  **参数解析**：解析新的 `<args>` XML 格式以识别所有目标文件及其相应的 diff 操作。它也可以处理传统的 `path`/`diff` 参数。
3.  **验证和批准**：
    *   验证所有目标文件是否存在且可访问（未被 `.rooignore` 阻止）。
    *   如果正在修改多个文件，则向用户显示**批量批准**对话框。
4.  **Diff 应用**：对于每个已批准的文件，使用 `MultiFileSearchReplaceDiffStrategy` 应用指定的 diff。此策略可以对单个文件应用多个、不重叠的更改。
5.  **结果**：返回汇总所有尝试操作结果的合并结果消息。

### 新的 Diff 格式（实验性）

实验模式在 `<apply_diff>` 工具调用中使用新的 XML 结构。

- **`<args>`**：所有文件操作的容器。
- **`<file>`**：每个要修改的文件的块。包含 `<path>` 和一个或多个 `<diff>` 标签。
- **`<path>`**：文件的相对路径。
- **`<diff>`**：包含更改的块。
    - **`<content>`**：`SEARCH/REPLACE` 块。
    - **`<start_line>`**：（可选）行号提示。

**示例：在一次调用中修改两个文件**

```xml
<apply_diff>
  <args>
    <file>
      <path>src/services/auth.service.ts</path>
      <diff>
        <content>
<<<<<<< SEARCH
:start_line:50
-------
    const token_expiration = '15m';
>>>>>>> REPLACE
        </content>
      </diff>
    </file>
    <file>
      <path>src/config/auth.config.ts</path>
      <diff>
        <content>
<<<<<<< SEARCH
:start_line:12
-------
    rateLimit: 5,
=======
    rateLimit: 10,
>>>>>>> REPLACE
        </content>
      </diff>
    </file>
  </args>
</apply_diff>
```