---
description: Roo Code Cloud 是使用 Roo Code 最简单的方式，无需额外账户和处理 API 密钥
keywords:
  - Roo Code Cloud
  - Roo Code Cloud Provider
  - LLM
  - Models
image: /img/social-share.jpg
---

# Roo Code Cloud Provider 概述

为了让使用 Roo Code 变得尽可能顺畅（Roo Code 依赖于 LLM 推理的提供商服务），我们构建了 Roo Code Cloud Provider。

你并非必须使用我们的提供商来使用 Roo Code（你可以从数十种提供商中选择），但这是最简单的方式，因为它只需要你的 Roo Code Cloud 账户，并提供我们测试和批准的模型选择：
- 来自顶级前沿实验室的尖端模型（包括 Anthropic、OpenAI、Google、xAI 等）
- 来自新兴实验室的测试版开源模型（Moonshot AI、MiniMax、GLM 等）

## 模型可用性

特定模型的可用性会随时间变化。我们努力保持列表相对简短，以便你知道无论选择哪个模型都可以放心使用。

你总能在[我们的网站](https://roocode.com/provider)或 Roo Code Cloud 应用的 ["Models"](https://app.roocode.com/models) 页面找到当前列表。

## 价格与隐私

我们绝不会将你的数据用于训练，也不会保留提示本身的日志
（请记住，如果你使用任务同步或 Cloud Agents，我们显然需要保留任务副本）。

有时会提供完全免费的隐身模型。这些通常是处于测试后期的高级模型，带有代号且可用性有限。这些模型很可能需要使用你的提示作为训练数据，因此使用时请多加注意。

付费模型很可能不会将你的数据用于训练，但最好还是查看供应商自身的隐私政策。

你总能在[我们的网站](https://roocode.com/provider)或 Roo Code Cloud 应用的 ["Models"](https://app.roocode.com/models) 页面找到当前定价。

:::info 寻找免费推理？
注册 Roo Code Cloud 账户时，你会获得一定数量的"免费分钟"来试用产品（你会看到一个可爱的小礼盒图标）。这些免费分钟涵盖 Cloud Agent 运行时间和通过 Roo Code Cloud Provider 的推理（如前所述，这需要消耗积分）。这些免费分钟无法在扩展中使用。
:::

## 如何使用

### Roo Code Cloud Agents

选择模型为你的 agent 提供动力时，只需选择 Roo Code Cloud Provider 即可。基本上不需要更多说明 :)

### Roo Code VS Code 扩展

确保你已在扩展中登录 Cloud 账户，就可以在 Provider Settings 中将 Roo 配置为提供商。

### 在第三方工具中

由于它是专为简化 Roo 使用而设计的，我们不会在其他产品中提供该提供商。没有 API 密钥供你复制到其他地方使用。