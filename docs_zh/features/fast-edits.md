---
description: 了解 Roo Code 的快速编辑功能如何使用差异比对实现更快、更安全的文件修改。学习匹配精度和配置选项。
keywords:
  - 快速编辑
  - 差异编辑
  - 文件修改
  - 应用差异
  - 匹配精度
  - 编辑效率
  - 防止截断
image: /img/social-share.jpg
---

# 差异/快速编辑

:::info 默认设置
快速编辑（启用“通过差异进行编辑”设置）在 Roo Code 中默认启用。除非遇到特定问题或想要尝试不同的差异策略，否则通常无需更改这些设置。
:::

Roo Code 提供了一项高级设置，通过使用差异（diffs）而非重写整个文件来更改文件编辑方式。启用此功能可带来显著优势。

:::note 按提供者设置
差异编辑配置在每个 [API 配置配置文件](/features/api-configuration-profiles) 中设置，允许您为不同的提供者和模型自定义编辑行为。
:::

---

## 启用通过差异进行编辑

点击齿轮图标 <Codicon name="gear" /> 打开 Roo Code 窗格设置。将显示 `Providers` 部分。选择您要配置的特定 [API 配置配置文件](/features/api-configuration-profiles)。

启用 **启用通过差异进行编辑** 后：

    <img src="/img/fast-edits/fast-edits-2.png" alt="Roo Code 设置显示启用通过差异进行编辑" width="500" />
1.  **更快的文件编辑**：Roo 通过仅应用必要的更改来更快速地修改文件。
2.  **防止截断写入**：系统会自动检测并拒绝 AI 写入不完整文件内容的尝试，这可能发生在大文件或复杂指令的情况下。这有助于防止文件损坏。

:::note 禁用快速编辑
如果您取消勾选 **启用通过差异进行编辑**，Roo 将恢复为使用 [`write_to_file`](/advanced-usage/available-tools/write-to-file) 工具重写整个文件内容进行每次编辑，而不是使用 [`apply_diff`](/advanced-usage/available-tools/apply-diff) 工具应用有针对性的更改。这种全写入方法通常修改现有文件较慢，并导致更高的令牌使用量。
:::

---

## 匹配精度

此滑块控制 AI 识别的代码部分在应用更改前必须与文件中的实际代码匹配的紧密程度。

    <img src="/img/fast-edits/fast-edits-4.png" alt="Roo Code 设置显示启用通过差异进行编辑复选框和匹配精度滑块" width="500" />

*   **100%（默认）**：需要完全匹配。这是最安全的选项，可最大程度降低错误更改的风险。
*   **较低值（80%-99%）**：允许“模糊”匹配。即使代码部分与 AI 预期的代码有微小差异，Roo 也可以应用更改。如果文件已被轻微修改，这可能很有用，但**会增加风险**，可能导致更改应用到错误的位置。

**谨慎使用低于 100% 的值。** 较低的精度有时可能是必要的，但请务必仔细审查建议的更改。

在内部，此设置会调整 `fuzzyMatchThreshold`，该阈值与 Levenshtein 距离等算法一起使用，以比较代码相似性。