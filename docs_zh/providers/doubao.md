---
sidebar_label: 豆包
description: 在 Roo Code 中配置字节跳动豆包 AI 模型。访问具有完整集成和国际化支持的竞争力语言模型。
keywords:
  - doubao
  - bytedance
  - bytedance ai
  - roo code
  - api provider
  - doubao models
  - chinese ai
  - language models
---

# 在 Roo Code 中使用豆包

豆包是字节跳动推出的中文 AI 服务，为各种开发任务提供具有竞争力的语言模型。该提供商包含完整的 API 集成，支持嵌入和国际化提示。

**网站：** [https://www.volcengine.com/](https://www.volcengine.com/)

---

## 获取 API 密钥

1. **注册/登录：** 访问 [火山引擎控制台](https://console.volcengine.com/)。创建账户或登录。
2. **导航至模型服务：** 在控制台中访问 AI 模型服务部分。
3. **创建 API 密钥：** 为豆包服务生成新的 API 密钥。
4. **复制密钥：** **重要：** 立即复制 API 密钥并安全存储。您可能无法再次查看它。

---

## 可用模型

Roo Code 支持通过字节跳动火山引擎 API 提供的所有豆包模型。

有关完整且最新的模型列表，请参阅 [火山引擎的 AI 模型服务](https://www.volcengine.com/)。

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 从“API 提供商”下拉菜单中选择“豆包”。
3. **输入 API 密钥：** 将您的豆包 API 密钥粘贴到“豆包 API 密钥”字段中。
4. **选择模型：** 从“模型”下拉菜单中选择您所需的模型。

**注意：** 豆包使用基础 URL `https://ark.cn-beijing.volces.com/api/v3`，服务器位于中国北京。