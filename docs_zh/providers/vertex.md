---
description: 通过 GCP Vertex AI 在 Roo Code 中访问 Google Gemini 和 Anthropic Claude 模型。配置身份验证并开始使用企业级 AI。
keywords:
  - Vertex AI
  - GCP
  - Google Cloud
  - Roo Code
  - Gemini
  - Claude
  - AI 模型
  - 机器学习
  - 云 AI
image: /img/social-share.jpg
sidebar_label: GCP Vertex AI
---

# 在 Roo Code 中使用 GCP Vertex AI

Roo Code 支持通过 Google Cloud Platform 的 Vertex AI 访问模型，Vertex AI 是一个托管的机器学习平台，提供对各种基础模型的访问，包括 Anthropic 的 Claude 系列。

**官网：** [https://cloud.google.com/vertex-ai](https://cloud.google.com/vertex-ai)

---

## 前置条件

*   **Google Cloud 账户：** 你需要一个活跃的 Google Cloud Platform (GCP) 账户。
*   **项目：** 你需要一个已启用 Vertex AI API 的 GCP 项目。
*   **模型访问权限：** 你必须请求并获得在 Vertex AI 上使用特定 Claude 模型的权限。请参阅 [Google Cloud 文档](https://cloud.google.com/vertex-ai/generative-ai/docs/partner-models/use-claude#before_you_begin) 了解操作说明。
*   **应用默认凭据 (ADC)：** Roo Code 使用应用默认凭据来与 Vertex AI 进行身份验证。最简单的方法是：
    1.  安装 Google Cloud CLI：[https://cloud.google.com/sdk/docs/install](https://cloud.google.com/sdk/docs/install)
    2.  使用命令进行身份验证：`gcloud auth application-default login`
*   **服务账号密钥（可选方式）：** 你也可以使用 Google Cloud 服务账号密钥文件进行身份验证。你需要在 GCP 项目中生成此密钥。请参阅 [Google Cloud 文档中关于创建服务账号密钥](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) 的说明。

---

## 可用模型

Roo Code 支持通过 Google Cloud Vertex AI 提供的所有模型，包括 Anthropic Claude、Google Gemini 和 MAAS（模型即服务）产品。

有关完整的、最新的模型列表和 ID，请参阅 [Vertex AI 的模型文档](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models)。

---

## 在 Roo Code 中的配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API Provider”下拉菜单中选择“GCP Vertex AI”。
3.  **配置身份验证：**
    
    Roo Code 使用以下身份验证优先级：
    1. **Google Cloud 凭据（JSON）：** 如果提供，此选项优先级最高
    2. **Google Cloud 密钥文件路径：** 如果提供且未提供 JSON 凭据，则使用此选项
    3. **应用默认凭据 (ADC)：** 当上述两者均未提供时，使用此选项作为回退
    
    **选项 1 - 使用 ADC（最简单）：**
    *   安装 Google Cloud CLI 并运行 `gcloud auth application-default login`
    *   Roo Code 中无需进一步配置
    
    **选项 2 - 使用服务账号密钥：**
    *   将 JSON 内容直接粘贴到 **Google Cloud Credentials** 字段中
    *   或者将文件路径提供到 **Google Cloud Key File Path** 字段中

4.  **输入项目 ID：** 输入你的 Google Cloud 项目 ID。
5.  **选择区域：** 选择你的 Vertex AI 资源所在的区域（例如 `us-east5`）。
6.  **选择模型：** 从“Model”下拉菜单中选择你想要的模型。

---

## 高级功能

### Gemini 特有功能

当通过 Vertex AI 使用 Gemini 模型时，会提供额外的 grounding 功能：

#### URL 上下文

启用 URL 上下文功能，允许 Gemini 模型直接访问和分析网页内容。此功能允许 Roo：

- 实时读取和理解网页
- 从 URL 分析文档
- 查看在线代码仓库
- 访问网站的当前信息

**启用 URL 上下文：**
1. 在你的 Vertex AI 配置中选择一个 Gemini 模型
2. 启用出现的“URL Context”选项
3. 保存你的设置

#### Google 搜索 Grounding

启用 Google 搜索 grounding 功能，通过实时搜索结果增强 Gemini 的响应。这提供了：

- 来自网络搜索的最新信息
- 事实核查能力
- 当前事件感知
- 技术查询的准确性增强

**启用搜索 Grounding：**
1. 在你的 Vertex AI 配置中选择一个 Gemini 模型
2. 启用出现的“Google Search Grounding”选项
3. 保存你的设置

:::note
URL 上下文和 Google 搜索 grounding 选项仅在选择 Gemini 模型时出现。这些功能可能产生额外费用。
:::

---

## 提示和注意事项

*   **权限：** 确保你的 Google Cloud 账户具有访问 Vertex AI 和你想要使用的特定模型所需的权限。
*   **定价：** 详情请参考 [Vertex AI 定价](https://cloud.google.com/vertex-ai/pricing) 页面。