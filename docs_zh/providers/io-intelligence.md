---
description: 本页介绍如何配置和使用 IO Intelligence 提供程序与 Roo Code 配合使用。
keywords:
  - io intelligence
  - provider
  - ai models
  - llama
  - deepseek
  - qwen
  - mistral
sidebar_label: IO Intelligence
---

# IO Intelligence 提供程序

IO Intelligence 提供程序通过统一的 API 为您提供对多种 AI 模型的访问权限，包括来自 Llama、DeepSeek、Qwen 和 Mistral 的模型。

## 配置

要使用 IO Intelligence 提供程序，您需要将其添加到 `~/.roo/config.json` 文件中。

1.  **获取 API 密钥**：您可以从 [IO Intelligence 网站](https://io.net/) 获取 API 密钥。
2.  **将提供程序添加到您的配置中**：将以下内容添加到您的 `config.json` 文件中：

```json
{
  "providers": [
    {
      "id": "io-intelligence",
      "apiKey": "YOUR_IO_INTELLIGENCE_API_KEY"
    }
  ]
}
```

## 可用模型

IO Intelligence 提供程序支持多种 AI 模型，包括 Llama、DeepSeek、Qwen 和 Mistral。

有关当前模型列表和规格，请参阅 [IO Intelligence 的文档](https://io.net/)。

您可以在 API 配置配置文件中指定模型，位置为 [`~/.roo/config.json`](#configuration)。