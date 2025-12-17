---
description: 了解模型上下文协议（MCP）及其如何使 AI 系统与外部工具交互。学习 MCP 架构和优势。
keywords:
  - what is MCP
  - Model Context Protocol
  - MCP architecture
  - AI tools integration
  - MCP client-server
  - JSON-RPC protocol
image: /img/social-share.jpg
sidebar_label: 什么是 MCP？
---

# 什么是 MCP？

MCP（Model Context Protocol，模型上下文协议）是一种标准化的通信协议，用于 LLM 系统与外部工具和服务进行交互。它作为 AI 助手与各种数据源或应用程序之间的通用适配器。

---

## 工作原理

MCP 采用客户端-服务器架构：

1. AI 助手（客户端）连接到 MCP 服务器
2. 每个服务器提供特定功能（文件访问、数据库查询、API 集成）
3. AI 通过标准化接口使用这些功能
4. 通信通过 JSON-RPC 2.0 消息进行

可以把 MCP 想象成类似于 USB-C 接口，任何兼容的 LLM 都可以连接到任何 MCP 服务器以访问其功能。这种标准化消除了为每个工具和服务构建自定义集成的需要。

例如，使用 MCP 的 AI 可以执行“搜索我们公司的数据库并生成报告”等任务，而无需为每个数据库系统编写专门的代码。

---

## 常见问题

- **MCP 是云服务吗？** MCP 服务器可以在本地计算机上运行，也可以作为云服务远程运行，具体取决于用例和安全要求。

- **MCP 会取代其他集成方法吗？** 不会。MCP 补充了现有的工具，如 API 插件和检索增强生成。它为工具交互提供了标准化协议，但不会取代专门的集成方法。

- **安全性如何处理？** 用户控制连接到哪些 MCP 服务器以及这些服务器拥有哪些权限。与任何访问数据或服务的工具一样，使用可信来源并配置适当的访问控制。

---

## Roo Code 中的 MCP

Roo Code 实现了模型上下文协议，用于：

- 连接本地和远程 MCP 服务器
- 提供访问工具的一致接口
- 在不修改核心代码的情况下扩展功能
- 按需启用专门功能

MCP 为 AI 系统与外部工具和服务的交互提供了一种标准化方式，使复杂的集成变得更加简单和一致。

---

## 进一步了解 MCP

准备深入了解了吗？查看这些指南：

- [MCP 概述](/features/mcp/overview) - 快速浏览 MCP 文档结构
- [在 Roo Code 中使用 MCP](/features/mcp/using-mcp-in-roo) - 在 Roo 中开始使用 MCP，包括创建简单的服务器
- [MCP 与 API 对比](/features/mcp/mcp-vs-api) - 与传统 API 相比的技术优势
- [STDIO 与可流式 HTTP 和 SSE 传输](/features/mcp/server-transports) - 本地与托管部署模型