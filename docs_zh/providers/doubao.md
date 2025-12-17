---
sidebar_label: Doubao
description: 在 Roo Code 中配置字节跳动的 Doubao AI 模型。通过完整的集成和国际化支持访问强大的语言模型。
keywords:
  - doubao
  - bytedance
  - bytedance ai
  - roo code
  - api provider
  - doubao models
  - chinese ai
  - language models
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Doubao

Doubao 是字节跳动推出的中文 AI 服务，提供具有竞争力的语言模型，适用于各类开发任务。该提供商支持完整的 API 集成，包含嵌入（embedding）功能和国际化提示（prompt）支持。

**官网：** [https://www.volcengine.com/](https://www.volcengine.com/)

---

## 获取 API Key

1. **注册/登录：** 访问 [火山引擎控制台](https://console.volcengine.com/)。注册账号或登录。
2. **导航至模型服务：** 在控制台中进入 AI 模型服务部分。
3. **创建 API Key：** 为 Doubao 服务生成新的 API Key。
4. **复制 Key：** **重要：** 立即复制 API Key 并安全保存。该 Key 可能无法再次查看。

---

## 可用模型

Roo Code 支持通过字节跳动火山引擎 API 提供的所有 Doubao 模型。

完整的最新模型列表，请参阅 [火山引擎 AI 模型服务](https://www.volcengine.com/)。

---

## 在 Roo Code 中的配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 在“API Provider”下拉菜单中选择“Doubao”。
3. **输入 API Key：** 将你的 Doubao API Key 粘贴到“Doubao API Key”字段中。
4. **选择模型：** 从“Model”下拉菜单中选择你想要使用的模型。

**注意：** Doubao 使用基础 URL `https://ark.cn-beijing.volces.com/api/v3`，服务器位于中国北京。