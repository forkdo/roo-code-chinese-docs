---
sidebar_label: 你的第一个任务
description: 学习如何使用 Roo Code AI 助手完成你的第一个任务。面向初学者的分步指南，了解审批工作流程和迭代过程。
keywords:
  - Roo Code 教程
  - 第一个任务
  - 入门指南
  - AI 编程助手教程
  - 审批工作流程
image: /img/social-share.jpg
---
import KangarooIcon from '@site/src/components/KangarooIcon';

# 你的第一个任务

在你已经[配置好 AI 提供商和模型](/getting-started/connecting-api-provider)之后，现在可以开始使用 Roo Code 了！本指南将带你完成首次交互的全过程。

---

## 步骤 1：打开 Roo Code 面板

点击 VS Code 活动栏（窗口侧边的垂直栏）中的 Roo Code 图标（<KangarooIcon />）以打开聊天界面。如果你看不到该图标，请确认扩展已安装并启用。

<figure>
  <img src="/img/your-first-task/your-first-task.png" alt="Roo Code 图标在 VS Code 活动栏中" width="600" />
  <figcaption>Roo Code 图标位于活动栏中，点击可打开聊天界面。你可以拖动它来调整位置。</figcaption>
</figure>

## 步骤 2：输入你的任务

在面板底部的聊天框中，输入你希望 Roo Code 执行的任务的清晰、简洁描述。以下是一些有效的任务示例：

* "创建一个名为 `hello.txt` 的文件，内容为 'Hello, world!'。"
* "编写一个 Python 函数，用于计算两个数的和。"
* "创建一个 HTML 文件，作为标题为 'Roo test' 的简单网站"

无需特殊命令或语法——只需使用自然语言即可。

<figure>
  <img src="/img/your-first-task/your-first-task-6.png" alt="在 Roo Code 聊天界面中输入任务" width="400" />
  <figcaption>在输入框中使用自然语言描述你的任务——无需特殊语法。</figcaption>
</figure>

## 步骤 3：发送任务

按 Enter 键或点击输入框右侧的发送图标（<Codicon name="send" />）来发送你的任务。

## 步骤 4：审查并批准操作

Roo Code 会分析你的请求并提出具体的操作建议。这些操作可能包括：

* **读取文件：** 显示需要访问的文件内容
* **写入文件：** 显示带有建议更改的差异对比（新增行用绿色，删除行用红色）
* **执行命令：** 显示将在终端中运行的确切命令
* **使用浏览器：** 概述浏览器操作（点击、输入等）
* **提出问题：** 在需要澄清时请求更多信息以继续推进

<figure>
  <img src="/img/your-first-task/your-first-task-7.png" alt="审查建议的文件创建操作" width="800" />
  <figcaption>Roo Code 会准确显示它想要执行的操作，并等待你的批准。</figcaption>
</figure>

**每个操作都需要你的明确批准**（除非启用了自动批准）：

* **批准：** 点击 "批准" 按钮以执行建议的操作
* **拒绝：** 点击 "拒绝" 按钮，如有需要可提供反馈

## 步骤 5：迭代

Roo Code 采用迭代方式工作。每个操作后，它会等待你的反馈，然后才会提出下一步操作。继续这个审查-批准循环，直到任务完成。

<figure>
  <img src="/img/your-first-task/your-first-task-8.png" alt="完成任务后的最终结果，展示迭代过程" width="500" />
  <figcaption>完成任务后，Roo Code 会显示最终结果并等待你的下一个指令。</figcaption>
</figure>

---

## 总结

你已经完成了与 Roo Code 的第一个任务！通过这个过程，你学会了：

* 如何使用自然语言与 Roo Code 交互
* 基于审批的工作流程，让你始终保持控制权
* Roo Code 用于逐步解决问题的迭代方法

这种基于审批的迭代工作流程是 Roo Code 的核心——让 AI 处理编码中的繁琐部分，同时你始终保持完全的监督。现在你已经掌握了基础知识，可以开始处理更复杂的任务，探索不同的[模式](/basic-usage/using-modes)以实现专业工作流程，或者尝试[自动批准功能](/features/auto-approving-actions)来加速重复性任务。