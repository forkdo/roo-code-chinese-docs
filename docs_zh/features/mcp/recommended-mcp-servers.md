---
description: 探索 Roo Code 推荐的 MCP 服务器，包括 Context7。学习如何安装和配置 MCP 服务器的分步说明。
keywords:
  - MCP 服务器
  - Context7
  - Roo Code MCP
  - MCP 安装
  - MCP 配置
  - 推荐服务器
image: /img/social-share.jpg
sidebar_label: 推荐的 MCP 服务器
---

# 推荐的 MCP 服务器

虽然 Roo Code 可以连接到任何遵循 Model Context Protocol (MCP) 规范的服务器，但社区已经构建了多个高质量的服务器，可直接使用。本页面精选了我们**积极推荐**的服务器，并提供分步设置说明，帮助您在几分钟内高效上手。

> 我们会持续更新此列表。如果您维护的服务器希望我们考虑添加，请提交 Pull Request。

---

## Context7

`Context7` 是我们首选的通用 MCP 服务器。它集成了多个高需求工具，通过单个命令即可安装，且在所有主流编辑器中均提供出色的 MCP 支持。

### 推荐 Context7 的原因

* **一键安装** – 所有功能已打包，无需本地构建步骤。
* **跨平台** – 支持 macOS、Windows、Linux 或 Docker 环境。
* **持续维护** – Upstash 团队频繁更新。
* **丰富工具集** – 包含数据库访问、网络搜索、文本工具等。
* **开源** – 采用 MIT 许可证发布。

---

## 在 Roo Code 中安装 Context7

有两种常见方式注册服务器：

1. **全局配置** – 在所有工作区中可用。
2. **项目级配置** – 与代码一起提交到版本控制。

以下将详细介绍两种方式。

### 1. 全局配置

1. 点击 <Codicon name="server" /> 图标，打开 Roo Code **MCP 设置**面板。
2. 点击 **Edit Global MCP**。
3. 将下方 JSON 粘贴到 `mcpServers` 对象中并保存。

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

**Windows (cmd.exe) 变体**

```json
{
  "mcpServers": {
    "context7": {
      "type": "stdio",
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

在 **Windows (cmd)** 上，您可能需要通过 `cmd.exe` 调用 `npx`：

<img src="/img/recommended-mcp-servers/context7-global-setup-fixed.png" alt="将 Context7 添加到全局 MCP 设置" width="600" />

### 2. 项目级配置

如果您希望将配置提交到仓库，请在项目根目录创建文件 `.roo/mcp.json` 并添加相同内容：

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

**Windows (cmd.exe) 变体**

```json
{
  "mcpServers": {
    "context7": {
      "type": "stdio",
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

<img src="/img/recommended-mcp-servers/context7-project-setup-fixed.png" alt="将 Context7 添加到项目级 MCP 文件" width="600" />

> 当全局和项目配置文件定义了同名服务器时，**项目配置优先**。

---

## 验证安装

1. 确保在 MCP 设置面板中已启用 **Enable MCP Servers**。
2. 此时应看到 **Context7** 列出。如果未运行，点击 <Codicon name="activate" /> 切换按钮启动。
3. Roo Code 首次调用 Context7 工具时会弹出提示。批准请求后继续。

<img src="/img/recommended-mcp-servers/context7-running-fixed.png" alt="Context7 在 Roo Code 中运行" width="400" />

---

## 后续步骤

* 在服务器面板中浏览 Context7 包含的工具列表。
* 为最常用的工具配置 **Always allow**，以简化工作流程。
* 想要暴露自己的 API？查看 [MCP 服务器创建指南](/features/mcp/using-mcp-in-roo#enabling-or-disabling-mcp-server-creation)。

需要其他服务器？关注本页面更新，我们将很快添加更多推荐！