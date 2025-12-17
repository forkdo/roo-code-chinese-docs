---
description: 了解 Roo Code 中的建议回复功能如何通过预设选项帮助您快速回答后续问题，提升工作效率。
keywords:
  - suggested responses
  - follow-up questions
  - quick answers
  - workflow optimization
  - ask_followup_question tool
image: /img/social-share.jpg
sidebar_label: 建议回复
---

import Codicon from '@site/src/components/Codicon';

# 建议回复

当 Roo 需要更多信息来完成任务时，它会使用 [`ask_followup_question` 工具](/advanced-usage/available-tools/ask-followup-question)。为了便于您更快速、更轻松地回复，Roo 通常会提供预设的回复选项。

---

## 概述

建议回复以可点击的按钮形式直接显示在聊天界面中 Roo 提出的问题下方。它们提供与问题相关的预设答案，帮助您快速提供输入。

<img src="/img/suggested-responses/suggested-responses.png" alt="Roo 提问并显示下方建议回复按钮的示例" width="500" />

---

## 工作原理

1.  **问题出现**：Roo 使用 `ask_followup_question` 工具提出问题。
2.  **显示建议**：如果 Roo 提供了建议选项，它们会以按钮形式显示在问题下方。
3.  **交互方式**：您可以通过两种方式与这些建议进行交互。

---

## 与建议选项的交互

您有三种方式使用建议回复：

1.  **直接选择**：
    *   **操作**：直接点击包含您想要提供答案的按钮。
    *   **结果**：选中的答案会立即作为您的回复发送给 Roo。如果某个建议完全符合您的意图，这是最快的回复方式。

2.  **键盘快捷键**：
    *   **操作**：使用您配置的键盘快捷键执行 `roo.acceptInput` 命令。
    *   **结果**：系统会自动选中主要（第一个）建议按钮。
    *   **注意**：详细设置信息，请参阅 [键盘快捷键](/features/keyboard-shortcuts)。

3.  **编辑后发送**：
    *   **操作**：
        *   按住 `Shift` 键并点击建议按钮。
        *   *或者*，将鼠标悬停在建议按钮上，点击出现的铅笔图标（<Codicon name="edit" />）。
    *   **结果**：建议的文本会被复制到聊天输入框中。然后您可以根据需要修改文本，再按 Enter 发送自定义的回复。当建议接近但需要微调时，这种方式非常有用。

<img src="/img/suggested-responses/suggested-responses-1.png" alt="聊天输入框显示从建议回复复制的文本，准备编辑" width="600" />

---

## 优势

*   **快速**：无需输入完整答案即可快速回复。
*   **清晰**：建议通常能澄清 Roo 需要的信息类型。
*   **灵活**：需要时可编辑建议，提供精确的自定义答案。

此功能简化了 Roo 需要澄清时的交互过程，让您能够以最少的努力高效引导任务完成。