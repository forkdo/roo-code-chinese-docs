---
description: 了解如何使用自定义指令来定制 Roo Code 的行为，以适应你的偏好、编码风格和项目需求。
keywords:
  - custom instructions
  - personalization
  - AI customization
  - coding preferences
  - project rules
image: /img/social-share.jpg
---

# 自定义指令

自定义指令允许你个性化 Roo 的行为，提供特定的指导来塑造回复、编码风格和决策过程。

:::info 指令文件位置
你可以通过全局规则（在所有项目中自动应用）、工作区规则（项目特定）或通过“提示”标签页界面来提供自定义指令。

**全局规则目录：** 自动应用于所有项目。
*   **Linux/macOS:** `~/.roo/rules/` 和 `~/.roo/rules-{modeSlug}/`
*   **Windows:** `%USERPROFILE%\.roo\rules\` 和 `%USERPROFILE%\.roo\rules-{modeSlug}\`

**工作区规则：** 仅应用于当前项目，当与全局规则冲突时优先。
*   **推荐方法：目录（`.roo/rules/`）**
    ```
    .
    ├── .roo/
    │   └── rules/          # 工作区范围规则
    │       ├── 01-general.md
    │       └── 02-coding-style.txt
    └── ... (其他项目文件)
    ```
*   **备用方法：单文件（`.roorules`）**
    ```
    .
    ├── .roorules           # 工作区范围规则（单文件）
    └── ... (其他项目文件)
    ```

**模式特定指令：** 仅应用于特定模式（例如 `code`）。
*   **推荐方法：目录（`.roo/rules-{modeSlug}/`）**
    ```
    .
    ├── .roo/
    │   └── rules-code/     # "code" 模式的规则
    │       ├── 01-js-style.md
    │       └── 02-ts-style.md
    └── ... (其他项目文件)
    ```
*   **备用方法：单文件（`.roorules-{modeSlug}`）**
    ```
    .
    ├── .roorules-code      # "code" 模式的规则（单文件）
    └── ... (其他项目文件)
    ```

规则按顺序加载：先全局规则，后工作区规则。如果发生冲突，工作区规则优先。详见 [全局规则目录](#全局规则目录)。
:::

---

## 什么是自定义指令？

自定义指令定义了超出 Roo 基本角色定义的特定行为、偏好和约束。示例包括编码风格、文档标准、测试要求和工作流指南。

---

## 设置自定义指令

### 全局自定义指令

这些指令在所有工作区中应用，无论你在处理哪个项目，都能保持你的偏好。

**如何设置：**

<img src="/img/custom-instructions/custom-instructions.png" alt="Roo Code 提示标签页显示全局自定义指令界面" width="600" />
1.  **打开提示标签页：** 点击 Roo Code 顶部菜单栏中的 <Codicon name="notebook" /> 图标
2.  **找到区域：** 找到“所有模式的自定义指令”区域
3.  **输入指令：** 在文本区域中输入你的指令
4.  **保存更改：** 点击“完成”保存更改

### 全局规则目录

全局规则目录功能提供可重用的规则和自定义指令，自动在所有项目中应用。此系统支持全局配置和项目特定覆盖。

#### 主要优势

**没有全局规则时：** 你必须在每个项目中维护单独的规则文件：
- 将相同的规则复制到每个新项目
- 在多个项目中手动更新规则
- 项目之间没有一致性

**有了全局规则：** 创建规则一次，处处使用：
- 为所有项目设置首选编码标准
- 在需要时为特定项目自定义特定规则
- 在所有工作中保持一致性
- 轻松为所有项目更新规则

#### 目录结构

全局规则目录位置是固定的，无法自定义：

**Linux/macOS：**
```
~/.roo/                           # 你的全局 Roo 配置
├── rules/                        # 应用于所有项目的通用规则
│   ├── coding-standards.md
│   ├── formatting-rules.md
│   └── security-guidelines.md
├── rules-code/                   # Code 模式特定规则
│   ├── typescript-rules.md
│   └── testing-requirements.md
├── rules-docs-extractor/         # 文档提取规则
│   └── documentation-style.md
└── rules-{mode}/                 # 其他特定模式的规则
    └── mode-specific-rules.md
```

**Windows：**
```
%USERPROFILE%\.roo\               # 你的全局 Roo 配置
├── rules\                        # 应用于所有项目的通用规则
│   ├── coding-standards.md
│   ├── formatting-rules.md
│   └── security-guidelines.md
├── rules-code\                   # Code 模式特定规则
│   ├── typescript-rules.md
│   └── testing-requirements.md
└── rules-{mode}\                 # 其他特定模式的规则
    └── mode-specific-rules.md
```

#### 设置全局规则

1. **创建全局规则目录：**
   ```bash
   # Linux/macOS
   mkdir -p ~/.roo/rules
   
   # Windows
   mkdir %USERPROFILE%\.roo\rules
   ```

2. **添加通用规则** (`~/.roo/rules/coding-standards.md`)：
   ```markdown
   # 全局编码标准
   
   1. 新项目始终使用 TypeScript
   2. 为所有新函数编写单元测试
   3. 使用描述性变量名
   4. 为公共 API 添加 JSDoc 注释
   ```

3. **添加模式特定规则** (`~/.roo/rules-code/typescript-rules.md`)：
   ```markdown
   # TypeScript Code 模式规则
   
   1. 在 tsconfig.json 中使用严格模式
   2. 对于对象形状，优先使用接口而非类型别名
   3. 始终指定函数的返回类型
   ```

#### 可用规则目录

| 目录 | 用途 |
|------|------|
| `rules/` | 应用于所有模式的通用规则 |
| `rules-code/` | Code 模式特定规则 |
| `rules-docs-extractor/` | 文档提取规则 |
| `rules-architect/` | 系统架构任务规则 |
| `rules-debug/` | 调试工作流规则 |
| `rules-{mode}/` | 任何自定义模式的规则 |

#### 规则加载顺序

规则按以下顺序加载：

1. **全局规则**（来自 `~/.roo/`）
2. **项目规则**（来自 `project/.roo/`）— 当冲突时优先于全局规则
3. [通用模式] **遗留文件**（工作区根目录 `.roorules`、`.clinerules`）— 仅在未加载通用规则目录内容时使用

在每个级别内，模式特定规则在通用规则之前加载。

### 工作区级别指令

这些指令仅在当前工作区中应用，允许你为特定项目自定义 Roo Code 的行为。

#### 通过文件/目录设置工作区范围指令

工作区范围指令应用于当前项目的 所有模式，可通过文件定义：

*   **推荐方法：基于目录（`.roo/rules/`）**
    *   在工作区根目录创建名为 `.roo/rules/` 的目录。
    *   在其中放置指令文件（例如 `.md`、`.txt`）。Roo Code 递归读取文件（包括子目录），按文件名的**字母顺序**将内容追加到系统提示中。
    *   当此目录存在且包含文件时，其内容与任何全局规则目录一起加载。
    *   注意：如果 `.roo/rules/` 目录存在但为空，Roo Code 将回退到使用 `.roorules` 文件。
*   **备用方法：基于文件（`.roorules`）**
    *   如果 `.roo/rules/` 不存在或为空，Roo Code 会在工作区根目录查找单个 `.roorules` 文件。
    *   如果找到，其内容将被加载。

#### 模式特定指令

模式特定指令可通过两种独立方式设置，可同时使用：

1.  **使用提示标签页：**

    <img src="/img/custom-instructions/custom-instructions-2.png" alt="Roo Code 提示标签页显示模式特定自定义指令界面" width="600" />
    * **打开标签页：** 点击 Roo Code 顶部菜单栏中的 <Codicon name="notebook" /> 图标
    * **选择模式：** 在“模式”标题下，点击要自定义的模式按钮
    * **输入指令：** 在“模式特定自定义指令（可选）”文本区域中输入指令
    * **保存更改：** 点击“完成”保存更改

        :::info 全局模式规则
        如果模式本身是全局的（非工作区特定），则为其设置的任何自定义指令也将在所有工作区中全局应用。
        :::

2.  **使用规则文件/目录：** 通过文件提供模式特定指令：
    *   **推荐方法：基于目录（`.roo/rules-{modeSlug}/`）**
        *   在工作区根目录创建名为 `.roo/rules-{modeSlug}/`（例如 `.roo/rules-docs-writer/`）的目录。
        *   在其中放置指令文件（递归加载，包括子目录）。文件按文件名的**字母顺序**读取并追加到系统提示中。
        *   当目录存在且包含文件时，此方法优先于备用文件方法。
    *   **备用方法：基于文件（`.roorules-{modeSlug}`）**
        *   如果 `.roo/rules-{modeSlug}/` 不存在或为空，Roo Code 会在工作区根目录查找单个 `.roorules-{modeSlug}` 文件（例如 `.roorules-code`）。
        *   如果找到，其内容将被加载到该模式。

来自提示标签页、全局规则、工作区规则和模式特定规则的指令将全部组合。详见下方部分了解确切顺序。

---

## 指令组合方式

指令按以下确切格式放置在系统提示中：

```
====
USER'S CUSTOM INSTRUCTIONS

The following additional instructions are provided by the user, and should be followed to the best of your ability without interfering with the TOOL USE guidelines.

Language Preference:
[如果设置了语言偏好]

Global Instructions:
[来自提示标签页的全局指令]

Mode-specific Instructions:
[来自提示标签页当前模式的模式特定指令]

Rules:

# Rules from rules-{modeSlug} directories:
[来自 ~/.roo/rules-{modeSlug}/ 和 .roo/rules-{modeSlug}/ 的所有文件内容（如果存在）]

# Rules from .roorules-{modeSlug}:
[来自 .roorules-{modeSlug} 文件的内容（如果模式特定目录没有文件）]

# Rules from .rooignore:
[如果适用，来自 .rooignore 的指令]

# Agent Rules Standard (AGENTS.md):
[来自工作区根目录的 AGENTS.md 或 AGENT.md 内容（如果存在且启用）]

# Rules from rules directories:
[来自 ~/.roo/rules/ 和 .roo/rules/ 的所有文件内容（如果存在）]

# Rules from .roorules:
[来自 .roorules 文件的内容（如果通用规则目录没有文件）]

====
```

*注意：系统从所有适用目录（全局 `~/.roo/` 和工作区 `.roo/`）加载规则，而非仅第一个有文件的目录。模式特定规则出现在通用规则之前。基于目录的规则仅在确定使用哪种方法时优先于基于文件的备用方法，但所有适用目录都会被读取。*

---

## 关于 .rules 文件的规则

* **文件位置：** 推荐方法使用 `.roo/` 内的目录（`.roo/rules/` 和 `.roo/rules-{modeSlug}/`）。备用方法使用单文件（`.roorules` 和 `.roorules-{modeSlug}`），位于工作区根目录。
* **递归读取：** 规则目录递归读取，包括子目录中的所有文件
* **文件过滤：** 系统自动排除缓存和临时文件（`.DS_Store`、`*.bak`、`*.cache`、`*.log`、`*.tmp`、`Thumbs.db` 等）
* **空文件：** 空或缺失的规则文件被静默跳过
* **源标题：** 基于目录的规则包含每文件标题 `# Rules from {绝对路径}:`，而基于文件的规则包含 `# Rules from {文件名}:` 标题
* **聚合：** 模式特定和通用规则的全局和工作区规则目录均被聚合（非二选一）
* **排序：** 文件仅按基名排序，不区分大小写
* **标题路径：** 标题路径为绝对路径，遵循符号链接
* **规则交互：** 模式特定规则补充全局规则，而非替换
* **符号链接：** 完全支持文件和目录的符号链接，最大解析深度为 5 以防止无限循环

---

## AGENTS.md 支持

Roo Code 还支持从工作区根目录的 `AGENTS.md`（或备用 `AGENT.md`）文件加载规则：

* **用途：** 提供 AI 行为的代理特定规则和指南
* **位置：** 必须在工作区根目录
* **加载：** 默认自动加载。要禁用 AGENTS.md 加载，在 VSCode 设置中设置 `"roo-cline.useAgentRules": false`
* **设置：** `roo-cline.useAgentRules`（默认：true）
* **优先级：** 如果两者都存在，优先使用 `AGENTS.md`
* **优先级：** 在模式特定规则和 `.rooignore` 之后、`~/.roo/rules` 和 `.roo/rules` 的通用规则之前加载
* **标题：** 添加到系统提示中，标题为 `# Agent Rules Standard (AGENTS.md):` 或 `(AGENT.md):`
* **空文件：** 空或仅空白的 `AGENTS.md` 被忽略
* **符号链接：** 符号链接到文件或目录在读取前解析

此功能允许团队维护可与项目代码一起版本控制的标准 AI 代理行为规则。

---

## 自定义指令示例

* "缩进始终使用空格，宽度为 4 个空格"
* "变量名使用驼峰命名法"
* "为所有新函数编写单元测试"
* "提供代码前先解释你的推理"
* "专注于代码的可读性和可维护性"
* "优先使用社区中最常见的库"
* "为网站添加新功能时，确保它们响应式且可访问"

:::tip 专业提示：团队标准化
对于团队环境，考虑以下方法：

**项目标准：** 在版本控制中使用工作区 `.roo/rules/` 目录为特定项目标准化 Roo 的行为。这确保团队成员之间一致的代码风格和开发工作流。

**组织标准：** 使用全局规则（`~/.roo/rules/`）建立适用于所有项目的组织范围编码标准。团队成员可设置相同的全局规则以实现所有工作的一致性。

**混合方法：** 结合全局规则以实现组织标准，使用项目特定工作区规则以满足项目特定需求。当规则冲突时，工作区规则优先。

基于目录的方法比单个 `.roorules` 文件提供更好的组织，并支持全局和项目级自定义。
:::

---

## 与自定义模式结合

对于高级自定义，将自定义指令与 [自定义模式](/features/custom-modes) 结合，创建具有特定工具访问、文件限制和定制指令的专业环境。