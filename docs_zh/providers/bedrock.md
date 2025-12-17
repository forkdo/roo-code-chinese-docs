---
sidebar_label: AWS Bedrock
description: 在 Roo Code 中使用 Amazon Bedrock 访问 Claude、Llama 等基础模型。配置凭据和 VPC 端点。
keywords:
  - aws bedrock
  - amazon bedrock
  - roo code
  - api provider
  - claude bedrock
  - llama bedrock
  - aws ai
  - foundation models
  - vpc endpoint
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 AWS Bedrock

Roo Code 支持通过 Amazon Bedrock 访问模型，Bedrock 是一项完全托管的服务，通过单一 API 提供来自领先 AI 公司的高性能基础模型（FM）。

**官网：** [https://aws.amazon.com/bedrock/](https://aws.amazon.com/bedrock/)

---

## 前置条件

*   **AWS 账户：** 需要一个活跃的 AWS 账户。
*   **Bedrock 访问权限：** 必须请求并获得 Amazon Bedrock 的访问权限。有关请求访问权限的详细信息，请参阅 [AWS Bedrock 文档](https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started.html)。
*   **模型访问权限：** 在 Bedrock 内，需要请求访问要使用的特定模型（例如 Anthropic Claude）。
*   **安装 AWS CLI：** 使用 AWS CLI 配置账户以进行身份验证
    ```bash
     aws configure
    ```

---

## 获取凭据

配置 AWS 凭据有两种主要方式：

1.  **AWS 访问密钥（推荐用于开发）：**
    *   创建一个具有必要权限的 IAM 用户（至少包含 `bedrock:InvokeModel`）。
    *   为该用户生成访问密钥 ID 和秘密访问密钥。
    *   （可选）如果您的 IAM 配置需要，请创建会话令牌。
2.  **AWS 配置文件：**
    *   使用 AWS CLI 或手动编辑 AWS 凭据文件来配置 AWS 配置文件。详细信息请参阅 [AWS CLI 文档](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)。

---

## 可用模型

Roo Code 支持 Amazon Bedrock 提供的所有基础模型。

有关模型 ID 和功能的完整、最新模型列表，请参阅 [AWS Bedrock 支持的模型文档](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html)。

**重要提示：** 在配置 Roo Code 时使用*模型 ID*，而不是模型名称。

---

## 在 Roo Code 中的配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标（<Codicon name="gear" />）。
2.  **选择提供商：** 从“API Provider”下拉菜单中选择“Bedrock”。
3.  **选择身份验证方式：**
    *   **AWS 凭据：**
        *   输入您的“A​WS Access Key”和“A​WS Secret Key”。
        *   （可选）如果使用临时凭据，请输入“A​WS Session Token”。
    *   **AWS 配置文件：**
        *   输入您的“A​WS Profile”名称（例如“default”）。
4.  **选择区域：** 选择您的 Bedrock 服务可用的 AWS 区域（例如“us-east-1”）。
5.  **（可选）跨区域推理：** 如果要访问与配置的 AWS 区域不同的区域中的模型，请勾选“Use cross-region inference”。
6.  **（可选）VPC 端点：** 适用于企业环境：
    *   勾选“Use VPC Endpoint”以通过您的 VPC 端点路由所有 Bedrock API 调用
    *   在出现的文本框中输入您的 VPC 端点 URL
    *   这确保所有 LLM 事务都保留在您的企业网络内
7.  **选择模型：** 从“Model”下拉菜单中选择您需要的模型。

---
---

## Claude 模型的推理预算

Roo Code 支持在 Bedrock 上为 Anthropic 的 Claude 模型使用推理预算（扩展思考）。这允许模型在响应前进行更多“思考”，对复杂任务很有用。

启用推理预算的方法：

1.  **选择支持推理功能的 Claude 模型**。
2.  **在模型设置中启用推理模式**。
3.  **调整思考预算**以控制模型的“思考”程度。

此功能仅适用于支持的 Claude 模型。

## 提示和注意事项

*   **权限：** 确保您的 IAM 用户或角色具有调用 Bedrock 模型的必要权限。需要 `bedrock:InvokeModel` 权限。
*   **定价：** 详细模型费用信息请参考 [Amazon Bedrock 定价](https://aws.amazon.com/bedrock/pricing/) 页面。
*   **跨区域推理：** 使用跨区域推理可能导致延迟增加。
*   **VPC 端点：** 使用 VPC 端点时，确保您的端点已正确配置以处理 Bedrock API 调用。此功能对有严格安全要求、强制将所有 API 流量保留在私有网络内的组织特别有用。