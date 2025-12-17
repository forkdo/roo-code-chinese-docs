---
description: 在 Roo Code 中配置 Vercel AI Gateway，通过统一接口稳健访问来自不同供应商的 100+ 个语言模型。
keywords:
  - roo code
  - vercel ai gateway
  - ai provider
  - language models
  - api configuration
  - model selection
  - prompt caching
  - usage tracking
  - byok
sidebar_label: Vercel AI Gateway
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Vercel AI Gateway

AI Gateway 提供了一个统一的 API，可通过单一端点访问数百个模型。它让你能够设置预算、监控使用情况、负载均衡请求以及管理降级策略。

有用的链接：
- 团队仪表板：https://vercel.com/d?to=%2F%5Bteam%5D%2F%7E%2Fai
- 模型目录：https://vercel.com/ai-gateway/models
- 文档：https://vercel.com/docs/ai-gateway

---

## 获取 API 密钥

需要 API 密钥进行身份验证。

1.  **注册/登录：** 访问 [Vercel 网站](https://vercel.com/) 并登录。
2.  **获取 API 密钥：** 前往 AI Gateway 选项卡中的 [API 密钥页面](https://vercel.com/d?to=%2F%5Bteam%5D%2F%7E%2Fai%2Fapi-keys&title=AI+Gateway+API+Key)。创建一个新密钥。
3.  **复制密钥：** 复制 API 密钥。

---

## 可用模型

Roo Code 会自动从 Vercel AI Gateway API 获取所有可用模型（来自多个供应商的数百个模型）。

如需查看包含能力的完整、最新的模型目录，请访问 [Vercel AI Gateway 模型页面](https://vercel.com/ai-gateway/models)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标（<Codicon name="gear" />）。
2.  **选择提供商：** 在“API Provider”下拉菜单中选择“Vercel AI Gateway”。
3.  **输入 API 密钥：** 将你的 Vercel AI Gateway API 密钥粘贴到“Vercel AI Gateway API Key”字段中。
4.  **选择模型：** 从“Model”下拉菜单中选择你想要的模型。

---

## 提示缓存
Vercel AI Gateway 支持为特定模型（包括 Anthropic Claude 和 OpenAI GPT 模型）自动缓存提示。这通过缓存常用提示来降低成本。

---

## 提示和注意事项

* **模型选择：** Vercel AI Gateway 提供了广泛的模型选择。请尝试找到最适合你需求的模型。
* **定价：** Vercel AI Gateway 根据底层模型的定价收费，包括缓存提示的费用。详情请见 [Vercel AI Gateway 模型页面](https://vercel.com/ai-gateway/models)。
* **Temperature：** 默认 temperature 为 `0.7`，可按模型配置。
* **自带密钥（BYOK）：** 如果你决定使用自己的密钥连接底层服务，Vercel AI Gateway **不收取附加费**。
* **更多信息：** Vercel 不会添加速率限制，但上游提供商可能会。新账户每 30 天获得 5 美元额度，直到首次付款为止。