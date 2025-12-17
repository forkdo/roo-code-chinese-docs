---
description: 在 Roo Code 中执行终端命令以进行系统操作、依赖安装、构建和开发工作流。
keywords:
  - execute_command
  - CLI commands
  - terminal
  - system operations
  - Roo Code tools
  - command execution
  - shell integration
image: /img/social-share.jpg
---

# execute_command

`execute_command` 工具用于在用户的系统上运行 CLI 命令。它允许 Roo 执行系统操作、安装依赖项、构建项目、启动服务器以及执行完成用户目标所需的其他基于终端的任务。

---

## 参数

该工具接受以下参数：

- `command`（必需）：要执行的 CLI 命令。必须对用户的操作系统有效。
- `cwd`（可选）：执行命令的工作目录。如果未提供，则使用当前工作目录。

---

## 功能说明

此工具直接在用户的系统上执行终端命令，支持从文件操作到运行开发服务器的广泛操作。命令在托管终端实例中运行，通过实时输出捕获与 VS Code 的终端系统集成，以实现最佳性能和安全性。

---

## 使用场景

- 安装项目依赖项时（npm install、pip install 等）
- 构建或编译代码时（make、npm run build 等）
- 启动开发服务器或运行应用程序时
- 初始化新项目时（git init、npm init 等）
- 执行其他工具无法提供的文件操作时
- 运行测试或代码检查操作时
- 需要为特定技术执行专用命令时

---

## 主要功能

- 与 VS Code shell API 集成，实现可靠的终端执行
- 通过注册表系统尽可能重用终端实例
- 逐行捕获命令输出，提供实时反馈
- 支持在后台继续运行的长时命令
- 允许指定自定义工作目录
- 在命令执行期间维护终端历史记录和状态
- 支持适合用户 shell 的复杂命令链
- 提供详细的命令完成状态和退出码解释
- 支持需要用户反馈循环的交互式终端应用程序
- 执行期间显示终端以确保透明度
- 使用 shell-quote 解析验证命令安全性
- 阻止潜在危险的子 shell 执行模式
- 与 RooIgnore 系统集成以实现文件访问控制
- 处理终端转义序列以获得干净输出

---

## 限制

- 命令访问可能受到 RooIgnore 规则和安全验证的限制
- 需要提升权限的命令可能需要用户配置
- 某些命令在不同操作系统上的行为可能有所不同
- 长时间运行的命令可能需要特殊处理
- 文件路径应根据操作系统 shell 规则正确转义
- 并非所有终端功能都适用于远程开发场景

---

## 工作原理

当调用 `execute_command` 工具时，它遵循以下流程：

1. **命令验证和安全检查**：
   - 使用 shell-quote 解析命令以识别组件
   - 根据安全限制验证（子 shell 使用、受限文件）
   - 对照 RooIgnore 规则检查文件访问权限
   - 确保命令满足系统安全要求

2. **终端管理**：
   - 通过 TerminalRegistry 获取或创建终端
   - 设置工作目录上下文
   - 准备输出捕获的事件监听器
   - 显示终端以确保用户可见性

3. **命令执行和监控**：
   - 通过 VS Code 的 shellIntegration API 执行
   - 使用转义序列处理捕获输出
   - 以 100ms 间隔节流输出处理
   - 监控命令完成或错误
   - 检测编译器等"热"进程以进行特殊处理

4. **结果处理**：
   - 去除 ANSI/VS Code 转义序列以获得干净输出
   - 使用详细的信号信息解释退出码
   - 如果命令更改了工作目录，则更新工作目录跟踪
   - 提供适当的上下文命令状态

---

## 终端实现细节

该工具使用了复杂的终端管理系统：

1. **优先级一：终端重用**
   - TerminalRegistry 尽可能重用现有终端
   - 这减少了终端实例的扩散并提高了性能
   - 终端状态（工作目录、历史记录）在命令间保持

2. **优先级二：安全验证**
   - 使用 shell-quote 解析命令以进行组件分析
   - 阻止危险模式，如 `$(...)` 和反引号
   - 根据 RooIgnore 规则检查命令的文件访问控制
   - 使用基于前缀的白名单系统验证命令模式

3. **性能优化**
   - 输出以 100ms 间隔节流处理，防止 UI 过载
   - 使用基于索引的跟踪实现零拷贝缓冲区管理
   - 为编译和"热"进程提供特殊处理
   - 为 Windows PowerShell 提供特定于平台的优化

4. **错误和信号处理**
   - 退出码映射到详细的信号信息（SIGTERM、SIGKILL 等）
   - 检测关键故障的核心转储
   - 跟踪并自动处理工作目录更改
   - 从终端断开连接场景中干净恢复

---

## 使用示例

- 设置新项目时，Roo 运行初始化命令，如 `npm init -y`，然后安装依赖项。
- 构建 Web 应用程序时，Roo 执行构建命令如 `npm run build` 来编译资源。
- 部署代码时，Roo 运行 git 命令提交并推送到仓库。
- 故障排除时，Roo 执行诊断命令以收集系统信息。
- 启动开发服务器时，Roo 启动适当的服务器命令（例如 `npm start`）。
- 运行测试时，Roo 执行项目测试框架的测试运行器命令。

---

## 使用示例

在当前目录中运行简单命令：
```
<execute_command>
<command>npm run dev</command>
</execute_command>
```

为项目安装依赖项：
```
<execute_command>
<command>npm install express mongodb mongoose dotenv</command>
</execute_command>
```

按顺序运行多个命令：
```
<execute_command>
<command>mkdir -p src/components && touch src/components/App.js</command>
</execute_command>
```

在特定目录中执行命令：
```
<execute_command>
<command>git status</command>
<cwd>./my-project</cwd>
</execute_command>
```

构建然后启动项目：
```
<execute_command>
<command>npm run build && npm start</command>
</execute_command>
```