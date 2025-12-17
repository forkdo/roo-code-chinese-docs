---
sidebar_label: Google Gemini
description: 在 Roo Code 中使用 Google Gemini AI 模型。配置 Gemini Flash、Pro 和实验性模型以优化你的开发工作流。
keywords:
  - google gemini
  - gemini ai
  - roo code
  - api provider
  - gemini flash
  - gemini pro
  - google ai
  - gemini models
  - ai studio
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Google Gemini

Roo Code 通过 Google AI Gemini API 支持 Google 的 Gemini 系列模型。

**官网：** [https://ai.google.dev/](https://ai.google.dev/)

---

## 获取 API 密钥

1.  **访问 Google AI Studio：** 导航至 [https://ai.google.dev/](https://ai.google.dev/)。
2.  **登录：** 使用你的 Google 账户登录。
3.  **创建 API 密钥：** 在左侧菜单中点击“创建 API 密钥”。
4.  **复制 API 密钥：** 复制生成的 API 密钥。

---

## 可用模型

Roo Code 支持 Google API 提供的所有 Gemini 模型，并自动跟踪 Google 最新的稳定版本。

完整的、最新的模型列表和功能说明，请参阅 [Google Gemini 模型文档](https://ai.google.dev/models/gemini)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标（<Codicon name="gear" />）。
2.  **选择提供商：** 在“API Provider”下拉菜单中选择“Google Gemini”。
3.  **输入 API 密钥：** 将你的 Gemini API 密钥粘贴到“Gemini API Key”字段中。
4.  **选择模型：** 从“Model”下拉菜单中选择你想要的 Gemini 模型。

默认情况下，Roo Code 会选择一个稳定的 Pro 模型，温度设置为 **1.0**（如果你的提供商支持）。这使得建议更具表现力和自然性，同时仍保持专注。如果你需要高度确定性的输出（例如，在 CI 中进行代码生成），可以将温度降低到接近 `0.0`。

---

## 高级功能

### URL 上下文

Gemini 模型现在可以通过 URL 上下文直接访问和分析网页内容。此功能允许 Roo 执行以下操作：

- 实时读取和理解网页
- 分析来自 URL 的文档
- 查看在线代码仓库
- 访问网站上的最新信息

#### 启用 URL 上下文

1. 打开 Roo Code 设置
2. 导航到 Gemini 提供商设置
3. 启用“URL Context”选项
4. 保存你的设置

#### 使用示例

```
请分析 https://example.com/api-docs 的文档，并根据 API 规范创建一个 TypeScript 客户端库。
```

### Google 搜索增强

启用 Google 搜索增强功能，可利用实时搜索结果提升 Gemini 的响应。这提供了：

- 来自网络搜索的最新信息
- 事实核查能力
- 对当前事件的感知
- 技术查询的更高准确性

#### 启用搜索增强

1. 打开 Roo Code 设置
2. 导航到 Gemini 提供商设置
3. 启用“Google Search Grounding”选项
4. 保存你的设置

#### 使用示例

```
2025 年 React Server Components 的最新最佳实践是什么？请搜索最新信息。
```

### 组合使用

两个功能可以结合使用，实现强大的工作流：

```
搜索最新的 Node.js 安全漏洞，然后分析我的 package.json 文件，看我是否受影响。同时查看官方 Node.js 安全页面的建议。
```

---

## 提示和注意事项

*   **定价：** Gemini API 使用按输入和输出 token 计费。URL 上下文和搜索增强功能可能产生额外费用。部分实验性模型可免费使用。详细定价信息请参考 [Gemini 定价页面](https://ai.google.dev/pricing)。
*   **模型选择：** 根据你的需求选择模型：
    - **Flash 模型：** 更快、更具成本效益，适用于大多数任务
    - **Pro 模型：** 更适合复杂推理和分析
    - **Thinking 模型：** 最适合需要逐步推理的任务（需要推理配额）
    - **实验性模型：** 最新功能，可能免费但稳定性较低
*   **上下文窗口：** 大多数 Gemini 模型支持高达 1,048,576 token 的上下文窗口，允许进行广泛的代码分析和文档处理。
*   **速率限制：** URL 上下文和搜索增强功能可能有独立的速率限制。请监控你的使用情况，避免触发限制。
*   **隐私：** 使用 URL 上下文时，请注意访问私有或敏感 URL。确保你有权分析相关内容。
*   **搜索质量：** Google 搜索增强在处理具体、结构良好的查询时效果最佳。明确你需要的信息。