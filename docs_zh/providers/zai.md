---
sidebar_label: Z AI
description: 在 Roo Code 中配置 Z AI 模型。通过区域感知路由访问 GLM 系列模型，支持国际用户和中国大陆用户。
keywords:
  - z ai
  - zai
  - zhipu ai
  - glm models
  - roo code
  - api provider
  - china ai
  - international ai
  - openai compatible
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Z AI

Z AI（智谱 AI）提供基于 GLM 系列的先进语言模型。该提供商具备区域感知路由功能，为国际用户和中国大陆用户提供独立的端点。

**官网：** [https://z.ai/model-api](https://z.ai/model-api)（国际）| [https://open.bigmodel.cn/](https://open.bigmodel.cn/)（中国）

---

## 获取 API 密钥

### 国际用户

1. **注册/登录：** 访问 [https://z.ai/model-api](https://z.ai/model-api)，创建账户或登录。
2. **进入 API 密钥页面：** 打开账户仪表盘，找到 API 密钥部分。
3. **创建密钥：** 为你的应用程序生成新的 API 密钥。
4. **复制密钥：** **重要：** 立即复制 API 密钥并安全保存。

### 中国大陆用户

1. **注册/登录：** 访问 [https://open.bigmodel.cn/](https://open.bigmodel.cn/)，创建账户或登录。
2. **进入 API 密钥页面：** 打开账户仪表盘，找到 API 密钥部分。
3. **创建密钥：** 为你的应用程序生成新的 API 密钥。
4. **复制密钥：** **重要：** 立即复制 API 密钥并安全保存。

---

## 可用模型

Roo Code 会根据你选择的区域自动从 Z AI 的 API 获取所有可用模型。

如需完整的、最新的模型列表和规格说明，请参阅官方提供商文档：
- **国际：** [Z AI 模型文档](https://z.ai/model-api)
- **中国大陆：** [BigModel 文档](https://open.bigmodel.cn/)

---

## 在 Roo Code 中的配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标（<Codicon name="gear" />）。
2. **选择提供商：** 从“API Provider”下拉菜单中选择“Z AI”。
3. **选择区域：** 选择你的区域：
   - “International”（默认）用于全球访问
   - “China”用于中国大陆访问
4. **输入 API 密钥：** 将 Z AI API 密钥粘贴到“Z AI API Key”字段中。
5. **选择模型：** 从“Model”下拉菜单中选择所需模型。可用模型取决于你选择的区域。

### 默认值与行为
- **自动 Base URL：** 所选区域自动确定 API 端点：
  - 国际 → `https://api.z.ai/api/paas/v4`
  - 中国 → `https://open.bigmodel.cn/api/paas/v4`
- **动态模型：** 更改区域会自动更新模型目录和目标端点。
- **无需手动 Base URL：** 在典型设置中，你通常不需要配置自定义 Base URL。

---

## 提示与注意事项

* **区域选择：** 区域设置决定 API 端点和可用模型：
  - 国际：使用 `https://api.z.ai/api/paas/v4`
  - 中国：使用 `https://open.bigmodel.cn/api/paas/v4`
* **自动 Base URL：** Base URL 由区域自动选择；在典型设置中无需手动覆盖。
* **OpenAI 兼容性：** Z AI 使用与 OpenAI 兼容的 API，提供流式响应和用量报告。
* **模型选择：** 模型会根据所选区域自动过滤，以确保兼容性。
* **需要 API 密钥：** 所有请求都需要有效的 API 密钥。确保你已从相应的区域平台获取密钥。
* **定价：** 请查看相应区域网站的当前定价信息。