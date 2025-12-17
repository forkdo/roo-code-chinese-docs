---
sidebar_label: Qwen Code CLI
description: 通过 OAuth 身份验证访问 Qwen3 Coder 模型。支持 1M 上下文窗口和自动令牌刷新。
keywords:
  - qwen code
  - qwen cli
  - qwen3 coder
  - roo code
  - api provider
  - oauth
  - alibaba
  - dashscope
image: /img/social-share.jpg
---

# Qwen Code CLI Provider

通过 OAuth 身份验证访问阿里巴巴的 Qwen3 Coder 模型，支持自动令牌刷新。具备专为大型代码库优化的 1M 标记上下文窗口。

:::info 需要设置
1. **安装 Qwen 客户端**：从官方网站下载
2. **身份验证**：运行客户端并登录以创建 OAuth 凭据
3. **在 Roo Code 中配置**：选择“Qwen Code CLI API”作为您的提供商
   - 默认路径 `~/.qwen/oauth_creds.json` 自动生效
   - 或根据需要指定自定义凭据路径
:::

**网站**：[https://chat.qwen.ai](https://chat.qwen.ai)

---

## 可用模型

Qwen3 Coder 模型具备 1M 上下文窗口和 65K 最大输出标记。

有关完整且最新的模型列表，请在 Roo Code 中配置提供商时查看 Qwen Code 提供商的模型目录。

---

## 配置

### OAuth 凭据路径
- **默认值**：`~/.qwen/oauth_creds.json`
- **支持自定义路径**：绝对路径和以 `~/` 开头的路径
- 使用 Qwen 客户端身份验证时自动创建

---

## 主要功能

- **OAuth 2.0**：安全的身份验证，支持自动令牌刷新
- **1M 上下文**：在单次对话中处理整个代码库
- **自动刷新**：令牌在 30 秒缓冲期内透明刷新
- **免费套餐**：每日 2,000 次请求和每分钟 60 次请求，无令牌限制，活动期间有效。
- **推理支持**：完全支持思维块

---

## 常见问题

**“找不到凭据文件”**
- 确保您已使用 Qwen 客户端进行身份验证
- 检查 `~/.qwen/oauth_creds.json` 文件是否存在

**“令牌刷新失败”**
- 检查网络连接
- 使用 Qwen 客户端重新身份验证

**“401 未授权”**
- 提供商应自动刷新（检查日志）
- 如果持续出现，请删除凭据并重新身份验证