---
description: 本页面说明如何配置和使用 IO Intelligence 提供商与 Roo Code 配合。
keywords:
  - io intelligence
  - provider
  - ai models
  - llama
  - deepseek
  - qwen
  - mistral
image: /img/social-share.jpg
sidebar_label: IO Intelligence
---

# IO Intelligence 提供商

IO Intelligence 提供商通过统一的 API，为您提供对多种 AI 模型的访问，包括来自 Llama、DeepSeek、Qwen 和 Mistral 的模型。

## 配置

要使用 IO Intelligence 提供商，您需要将其添加到您的 `~/.roo/config.json` 文件中。

1.  **获取您的 API 密钥**：您可以通过 [IO Intelligence 官网](https://io.net/) 获取 API 密钥。
2.  **将提供商标识添加到配置中**：在您的 `config.json` 文件中添加以下内容：

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

IO Intelligence 提供商支持多种 AI 模型，包括 Llama、DeepSeek、Qwen 和 Mistral。

有关当前模型列表和详细规格，请参阅 [IO Intelligence 的文档](https://io.net/)。

您可以在 [`~/.roo/config.json`](#configuration) 中的 API 配置文件中指定模型。