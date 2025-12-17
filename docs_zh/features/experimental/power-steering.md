---
sidebar_label: 'Power Steering'
description: '通过 Power Steering 提升 Roo Code 的响应一致性。这个实验性功能会强化模式定义和自定义指令，以更好地遵循分配的角色。'
keywords:
  - power steering
  - LLM 一致性
  - 模式遵循
  - 自定义指令
  - 实验性功能
  - token 优化
  - 角色定义
image: /img/social-share.jpg
---
import Codicon from '@site/src/components/Codicon';

# Power Steering（实验性功能）

"Power Steering" 实验性功能（`POWER_STEERING`）旨在通过更频繁地提醒底层大语言模型（LLM）其当前模式定义和任何自定义指令，来增强 Roo Code 响应的一致性。

---

## 工作原理

启用 Power Steering 后，Roo Code 会持续强化 LLM 对其分配角色（例如"你是一个有用的编程助手"）以及用户提供的任何特定指南（例如"始终提供 Python 代码示例"）的理解。

这是通过在每次交互时，将 `modeDetails.roleDefinition` 和 `modeDetails.customInstructions` 明确包含在发送给 LLM 的信息中来实现的。

**目标：**
主要目标是确保 LLM 更严格地遵循其定义的角色，并更一致地执行用户特定的指令。如果你发现 Roo 偏离其角色或忽略自定义规则，Power Steering 可以帮助保持其专注度。

**权衡：**
这些频繁的提醒会消耗每次发送给 LLM 消息中的额外 token。这意味着：
*   每条消息的 token 使用量增加。
*   潜在的运营成本增加。
*   上下文窗口可能更快被填满。

这是在更严格的指令遵循和资源消耗之间的一种平衡。

**默认状态：** 已禁用。

---

## 技术细节

*   **实验 ID：** `powerSteering`
*   **机制：**
    *   该功能的状态由 `getEnvironmentDetails` 函数检查。
    *   如果启用，当前模式的 `roleDefinition` 和 `customInstructions` 会被添加到发送给 LLM 的详细信息中。
    *   这些详细信息被包装在 `<environment_details>` 标签中，成为每次 LLM 交互上下文的一部分。
*   **影响：** 通过频繁包含角色定义和自定义指令，LLM 被引导生成更符合这些参数的响应。

---

## 启用此功能

Power Steering 在 Roo Code 高级设置的"实验性功能"部分中管理。

1.  打开 Roo Code 设置（右上角的 <Codicon name="gear" /> 图标）。
2.  导航到"高级设置"。
3.  找到"实验性功能"区域。
4.  切换"Power Steering"选项。
5.  保存你的更改。
<img src="/img/power-steering/power-steering.png" alt="智能上下文压缩和 Power Steering 的设置" width="600" />

有关实验性功能的一般信息，请参阅[实验性功能概述](/features/experimental/experimental-features)。

---

## 反馈

请在 [Roo Code GitHub Issues 页面](https://github.com/RooCodeInc/Roo-Code/issues) 上报告有关此功能的任何问题或建议。你的反馈对改进 Roo Code 至关重要。