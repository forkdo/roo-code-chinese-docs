---
description: 了解 Roo Code 如何与你的 Shell 集成以执行命令。终端问题和 Shell 配置的故障排除指南。
keywords:
  - shell 集成
  - 终端命令
  - 命令执行
  - shell 配置
  - 故障排除
image: /img/social-share.jpg
---

# 终端 Shell 集成

终端 Shell 集成是 Roo Code 的一项核心功能，它使 Roo Code 能够在你的终端中执行命令并智能地处理其输出。这种 AI 与你的开发环境之间的双向通信解锁了强大的自动化能力。

---

## 什么是 Shell 集成？

Shell 集成在 Roo Code 中自动启用，它直接连接到你终端的命令执行生命周期，无需你进行任何设置。这个内置功能让 Roo 能够：

- 通过 [`execute_command`](/advanced-usage/available-tools/execute-command) 工具代表你执行命令
- 实时读取命令输出，无需手动复制粘贴
- 自动检测并修复运行中应用程序的错误
- 观察命令退出码以确定成功或失败
- 跟踪工作目录变化，当你在项目中导航时
- 智能响应终端输出，无需用户干预
- 从聊天界面直接停止正在运行的命令，方法是点击命令执行消息旁出现的停止按钮

<img src="/img/v3.15/v3.15.png" alt="聊天 UI 中的停止命令按钮" width="600" />

当你要求 Roo 执行诸如安装依赖、启动开发服务器或分析构建错误等任务时，Shell 集成在后台工作，使这些交互变得流畅高效。

---
 

## 终端集成设置

Roo Code 提供了设置来微调它与终端的交互方式。要访问这些设置：
1. 点击 Roo Code 侧边栏右上角的 <Codicon name="gear" /> 图标。
2. 在打开的设置面板中，从左侧菜单选择“Terminal”组。

### 基础设置

#### 终端输出限制
<img src="/img/shell-integration/shell-integration-13.png" alt="终端输出限制滑块设置为 500" width="600" />
按行截断。Roo 保留开头和结尾，中间部分被省略，用 "[...N lines omitted...]" 标记，以保持在限制内。机制：保留约 20% 的头部和 80% 的尾部允许行预算，并插入省略标记，保留尾部前的空行以提高可读性。适用于命令打印多行（例如长日志）且你主要关心头部和最终结果时。当中间细节重要时避免使用。默认值：500 行。

#### 终端字符限制
<img src="/img/shell-integration/shell-integration-15.png" alt="终端字符限制设置" width="600" />
对总输出大小（字符）的硬性限制。Roo 保留开头和结尾，中间部分用 "[...N characters omitted...]" 标记省略。机制：优先于行限制；保留约 20% 的头部和约 80% 的尾部字符预算，覆盖行限制以防止极长行或巨大块导致内存问题。适用于命令打印极长行或巨大块时。仅在需要确切完整内容时禁用。

#### 压缩进度条输出
<img src="/img/shell-integration/shell-integration-14.png" alt="压缩进度条输出复选框" width="600" />
开启：通过处理回车符（\r）和退格符（\b）折叠进度条/旋转器，只保留最终状态，然后应用游程编码压缩重复行。关闭：保持每个更新的确切打印。当你不需要中间旋转器状态时使用（推荐开启）。仅在调试逐步进度行为时禁用。

### 高级设置

除非另有说明，这些设置仅在“使用内联终端（推荐）”关闭时生效（即使用 VS Code 终端）。

:::info 重要
**终端重启以应用这些设置**

高级终端设置的更改仅在重启终端后生效。要重启终端：

1. 点击终端面板中的垃圾桶图标关闭当前终端
2. 使用 Terminal → New Terminal 或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（反引号）打开新终端

更改任何这些设置后，始终重启所有打开的终端。
:::

<a id="use-inline-terminal-recommended"></a>
<a id="disable-terminal-shell-integration"></a>
#### 使用内联终端（推荐）
<img src="/img/shell-integration/shell-integration-16.png" alt="使用内联终端（推荐）开关" width="600" />
控制 Roo Code 如何执行终端命令。

- 开启（使用内联终端）：使用内联终端（在聊天中）运行命令，绕过 Shell 配置文件和 VS Code Shell 集成，以获得可靠性和更快的启动。机制：使用后台“execa”提供者并直接流式传输输出（无 VS Code OSC 633/133 标记）。

    <img src="/img/shell-integration/shell-integration-12.png" alt="Roo Code 内联终端，当'使用内联终端（推荐）'开启时" width="600" />
    *内联终端激活（使用内联终端开启）。*

- 关闭（使用 VS Code 终端）：使用 VS Code 集成终端和你的 Shell 配置文件；可能需要 Shell 集成，更可能遇到“Shell 集成不可用”问题。仅在你需要终端 UI 功能或交互式配置文件行为时使用此选项。

#### 决策指南：内联终端开启 vs 关闭
- 当你想要可靠性、更快启动或你的 Shell 配置文件导致问题时，使用开启。
- 当你需要终端 UI 功能或你的 Shell 提示自定义运行时，使用关闭。
- 提示：如果终端命令失败或卡住，切换到开启并重试。

:::info 运行时环境
在 macOS（可能还有其他操作系统）上，提供给 VS Code 和 Roo Code 的环境可能因 VS Code 的启动方式而异。

如果从命令行使用 `code` 命令启动，VS Code 和 Roo Code 会从启动它的 Shell 继承环境。

如果从 Finder、Dock 或 Spotlight 启动，从 `.zshrc` 或 `.zprofile` 导出的环境可能缺失。

如果你依赖这些文件中的环境变量且它们在 VS Code 中缺失，请将它们移到 `.zshenv`，然后注销并重新登录，以便窗口管理器获取新设置。
:::

以下高级设置仅在关闭时生效（即使用 VS Code 终端）：

#### 继承环境变量
<img src="/img/shell-integration/shell-integration-17.png" alt="继承环境变量复选框" width="600" />
仅 VS Code 终端。控制 VS Code 集成终端是否从父 VS Code 进程继承环境变量。镜像 VS Code 设置 [`terminal.integrated.inheritEnv`](https://code.visualstudio.com/docs/editor/integrated-terminal#_inherit-environment-variables)。注意：内联终端（“使用内联终端（推荐）”开启）作为后台进程运行，始终使用扩展的 Node 进程环境；此设置不影响它。如果你依赖 VS Code 提供的 PATH/代理/身份验证变量，请保持启用（VS Code 默认）。仅在需要干净、可重现的集成终端会话或调试环境冲突时禁用。

#### 终端 Shell 集成超时
<img src="/img/shell-integration/shell-integration-18.png" alt="终端 Shell 集成超时滑块设置为 15s" width="600" />
Roo 等待 VS Code Shell 集成初始化和集成流启动的时间。如果在超时内未就绪，将发出“无 Shell 集成”事件，重试时执行将回退到内联终端。当你使用 Shell/配置文件有长启动时间或看到“Shell 集成不可用”错误时使用。如果你使用内联终端（不适用），避免增加。默认值：15s。仅在使用 VS Code 终端时适用。

#### 终端命令延迟
<img src="/img/shell-integration/shell-integration-19.png" alt="终端命令延迟滑块设置为 0ms" width="600" />
在每个命令后添加小延迟，以帮助 VS Code 终端刷新所有输出。机制：为 bash/zsh 设置 `PROMPT_COMMAND='sleep N'`，为 PowerShell 附加 `start-sleep -milliseconds N`。当你看到截断/缺失尾部输出或提示竞争时使用。当输出捕获看起来正确时避免使用。设置为 0 以禁用。默认值：0ms。

#### 启用 PowerShell 计数器变通方案
<img src="/img/shell-integration/shell-integration-20.png" alt="启用 PowerShell 计数器变通方案复选框" width="600" />
开启：附加 `; "(Roo/PS Workaround: N)" > $null` 到每个命令，以强制可靠的执行后信号，避免在某些设置上输出不完整或重复，或连续运行同一命令两次失败。使用当你使用 Windows PowerShell 且输出不完整或重复，或连续运行同一命令两次失败时。关闭：以未更改方式运行 PowerShell 命令。

#### 清除 ZSH EOL 标记
<img src="/img/shell-integration/shell-integration-21.png" alt="清除 ZSH EOL 标记复选框" width="600" />
开启：省略 Zsh 的行尾标记 (%)，以便正确解析输出。机制：设置 `PROMPT_EOL_MARK=""`。当你捕获的输出以杂散 % 结尾或解析看起来错误时使用。关闭：保留默认 EOL 标记（在某些设置上可能混淆解析）。

#### 启用 Oh My Zsh 集成
<img src="/img/shell-integration/shell-integration-22.png" alt="启用 Oh My Zsh 集成复选框" width="600" />
适用于使用流行的 Oh My Zsh 框架的 Zsh 用户。如果你使用 Oh My Zsh 并遇到终端命令执行或输出渲染的一般问题，且其他设置无法解决，请启用此选项。这有助于 Roo Code 与 Oh My Zsh 的特定 Shell 集成机制对齐，通过设置 `ITERM_SHELL_INTEGRATION_INSTALLED=Yes`。可能需要重启 IDE。

#### 启用 Powerlevel10k 集成
<img src="/img/shell-integration/shell-integration-23.png" alt="启用 Powerlevel10k 集成复选框" width="600" />
适用于使用 Zsh 的 Powerlevel10k 主题的用户。如果你复杂的 Powerlevel10k 提示符似乎干扰 Roo Code 正确检测命令边界、解析输出或跟踪当前工作目录的能力，请启用此选项。这设置 `POWERLEVEL9K_TERM_SHELL_INTEGRATION=true`。

#### 启用 ZDOTDIR 处理
<img src="/img/shell-integration/shell-integration-24.png" alt="启用 ZDOTDIR 处理复选框" width="600" />
开启：使用临时 ZDOTDIR，以便 VS Code Shell 集成与 zsh 一起工作，同时保留你的配置。机制：创建一个临时目录，其中包含一个 `.zshrc`，它引用 VS Code 的 Shell 集成脚本，然后重新引用你的原始 zsh 文件并重置 ZDOTDIR；临时目录在初始化后被清理。当你遇到 zsh Shell 集成失败或与你的点文件冲突时使用。关闭：使用你的正常 ZDOTDIR。

---

## Shell 集成工作原理

Shell 集成将 Roo 连接到你的终端命令执行过程，实时进行：

1. **连接**：当你打开终端时，VS Code 与你的 Shell 建立特殊连接。

2. **命令跟踪**：VS Code 通过检测以下内容来监控你的终端活动：
   - 新提示符出现时
   - 你输入命令时
   - 命令开始运行时
   - 命令完成时（以及是否成功或失败）
   - 你当前所在的目录

3. **不同 Shell，相同结果**：每种 Shell 类型（Bash、Zsh、PowerShell、Fish）在后台实现略有不同，但它们都为 Roo 提供相同的功能。

4. **信息收集**：Roo 可以看到正在运行的命令、它们在哪里运行、运行时间、是否成功以及它们的完整输出——所有这些都不需要你复制粘贴任何内容。

---

## Shell 集成故障排除

#### 快速修复
1. 更新 VS Code/Cursor 到最新版本（需要 VS Code 1.93+）。
2. 命令面板（Ctrl+Shift+P / Cmd+Shift+P）→ “Terminal: Select Default Profile” → 选择 bash、zsh、PowerShell 或 fish。
3. Windows PowerShell：运行 `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`，然后重启 VS Code。
4. WSL（bash）：在 `~/.bashrc` 中添加 `. "$(code --locate-shell-integration-path bash)"`。

#### PowerShell 执行策略（Windows）

PowerShell 默认限制脚本执行。要配置：

1. 以管理员身份打开 PowerShell
2. 检查当前策略：`Get-ExecutionPolicy`
3. 设置适当策略：`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`

常见策略：
- `Restricted`：不允许脚本（默认）
- `RemoteSigned`：本地脚本可以运行；下载的脚本需要签名
- `Unrestricted`：所有脚本运行并有警告
- `AllSigned`：所有脚本必须签名

#### 手动 Shell 集成安装

如果自动集成失败，在你的 Shell 配置中添加适当的行：

**Bash** (`~/.bashrc`)：
```bash
[[ "$TERM_PROGRAM" == "vscode" ]] && . "$(code --locate-shell-integration-path bash)"
```

**Zsh** (`~/.zshrc`)：
```zsh
[[ "$TERM_PROGRAM" == "vscode" ]] && . "$(code --locate-shell-integration-path zsh)"
```

**PowerShell** (`$Profile`)：
```powershell
if ($env:TERM_PROGRAM -eq "vscode") { . "$(code --locate-shell-integration-path pwsh)" }
```

**Fish** (`~/.config/fish/config.fish`)：
```fish
string match -q "$TERM_PROGRAM" "vscode"; and . (code --locate-shell-integration-path fish)
```

#### 终端自定义问题

如果你使用终端自定义工具：

**Powerlevel10k**：
```bash
# 在 ~/.zshrc 中引用 powerlevel10k 之前添加
typeset -g POWERLEVEL9K_TERM_SHELL_INTEGRATION=true
```

**替代方案**：在 Roo Code 中启用 Powerlevel10k 集成设置。

#### 验证 Shell 集成状态

使用以下命令确认 Shell 集成处于活动状态：

**Bash**：
```bash
set | grep -i '[16]33;'
echo "$PROMPT_COMMAND" | grep vsc
trap -p DEBUG | grep vsc
```

**Zsh**：
```zsh
functions | grep -i vsc
typeset -p precmd_functions preexec_functions
```

**PowerShell**：
```powershell
Get-Command -Name "*VSC*" -CommandType Function
Get-Content Function:\Prompt | Select-String "VSCode"
```

**Fish**：
```fish
functions | grep -i vsc
functions fish_prompt | grep -i vsc
```

Shell 集成活动的视觉指示器：
1. 终端标题栏中的 Shell 集成指示器
2. 命令检测高亮
3. 终端标题中的工作目录更新
4. 命令持续时间和退出码报告

---

#### WSL：最佳实践设置

使用 Windows 子系统 Linux（WSL）时，有两种不同的方式在 VS Code 中使用 WSL，每种方式对 Shell 集成都有不同的影响：

#### 方法 1：VS Code Windows 与 WSL 终端

在此设置中：
- VS Code 在 Windows 中本地运行
- 你使用 VS Code 中的 WSL 终端集成功能
- Shell 命令通过 WSL 桥执行
- 由于 Windows-WSL 通信，可能出现额外延迟
- Shell 集成标记可能受 WSL-Windows 边界影响：你必须确保在 WSL 环境中为你的 Shell 加载了 `source "$(code --locate-shell-integration-path <shell>)"`，因为它可能不会自动加载；见上文。

#### 方法 2：在 WSL 中运行的 VS Code

在此设置中：
- 你直接从 WSL 中使用 `code .` 启动 VS Code
- VS Code 服务器在 Linux 环境中本地运行
- 直接访问 Linux 文件系统和工具
- Shell 集成性能和可靠性更好
- Shell 集成自动加载，因为 VS Code 在 Linux 环境中本地运行
- 推荐用于 WSL 开发

对于 WSL 的最佳 Shell 集成，我们建议：
1. 打开你的 WSL 发行版
2. 导航到你的项目目录
3. 使用 `code .` 启动 VS Code
4. 在 VS Code 中使用集成终端

---


#### Cygwin（bash、zsh）

Cygwin 在 Windows 系统上提供类 Unix 环境。要在 VS Code 中将 Cygwin 配置为你的终端：

1. 从 [https://www.cygwin.com/](https://www.cygwin.com/) 安装 Cygwin

2. 打开 VS Code 设置：
   - 选择 File > Preferences > Settings
   - 点击右上角的“Open Settings (JSON)”图标
   
3. 在 `settings.json` 中添加以下配置（在顶级大括号 `{}` 内）：
   ```json
   {
     "terminal.int