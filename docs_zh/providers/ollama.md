---
sidebar_label: Ollama
description: 在 Roo Code 中设置 Ollama，以在本地运行开源大语言模型，实现隐私保护、离线访问和经济高效的 AI 编程。
keywords:
  - Ollama
  - 本地模型
  - Roo Code
  - 开源 AI
  - CodeLlama
  - Qwen
  - 离线 AI
  - 隐私
  - 上下文窗口配置
image: /img/social-share.jpg
---
import KangarooIcon from '@site/src/components/KangarooIcon';

# 在 Roo Code 中使用 Ollama

Roo Code 支持使用 Ollama 在本地运行模型。这提供了隐私保护、离线访问以及潜在的更低成本，但需要更多的设置工作和一台性能强大的计算机。

**官网：** [https://ollama.com/](https://ollama.com/)

---

## 设置 Ollama

1.  **下载并安装 Ollama：** 从 [Ollama 官网](https://ollama.com/) 下载适用于您操作系统的 Ollama 安装程序。按照安装说明进行操作。确保 Ollama 正在运行。

    ```bash
    ollama serve
    ```

2.  **下载模型：** 浏览 [Ollama 模型库](https://ollama.com/library) 查看所有可用模型。要下载模型，请运行：

    ```bash
    ollama pull <model_name>
    ```

    例如：

    ```bash
    ollama pull qwen2.5-coder:32b
    ```

3. **配置模型：** 在 Ollama 中配置模型的上下文窗口并保存一份副本。

   :::info 默认上下文行为
   **Roo Code 默认自动遵循 Modelfile 中的 `num_ctx` 设置。** 当您在 Ollama 中使用模型时，Roo Code 会读取模型配置的上下文窗口并自动使用。您无需在 Roo Code 设置中配置上下文大小 — 它会自动遵循您在 Ollama 模型中定义的内容。
   :::

   **选项 A：交互式配置**
   
   加载模型（我们以 `qwen2.5-coder:32b` 为例）：
   
    ```bash
    ollama run qwen2.5-coder:32b
    ```

   更改上下文大小参数：

    ```bash
    /set parameter num_ctx 32768
    ```

    使用新名称保存模型：

    ```bash
    /save your_model_name
    ```

   **选项 B：使用 Modelfile（推荐）**

   创建一个包含您所需配置的 `Modelfile`：

   ```dockerfile
   # 示例 Modelfile，设置较小的上下文
   FROM qwen2.5-coder:32b
   
   # 将上下文窗口设置为 32K tokens（从默认值减少）
   PARAMETER num_ctx 32768
   
   # 可选：调整温度以获得更一致的输出
   PARAMETER temperature 0.7
   
   # 可选：设置重复惩罚
   PARAMETER repeat_penalty 1.1
   ```

   然后创建您的自定义模型：

   ```bash
   ollama create qwen-32k -f Modelfile
   ```

   :::tip 覆盖上下文窗口
   如果需要覆盖模型的默认上下文窗口：
   - **永久性：** 使用所需的 `num_ctx` 保存模型的新版本（通过上述任一方法）
   - **Roo Code 行为：** Roo 自动使用 Ollama 模型中配置的 `num_ctx`
   - **内存考虑：** 减少 `num_ctx` 有助于防止在有限硬件上出现内存溢出错误
   :::

4.  **配置 Roo Code：**
    *   打开 Roo Code 侧边栏（<KangarooIcon /> 图标）。
    *   点击设置齿轮图标（<Codicon name="gear" />）。
    *   选择 "ollama" 作为 API 提供商。
    *   输入上一步中保存的模型标签或名称（例如 `your_model_name`）。
    *   （可选）如果您在其他机器上运行 Ollama，请配置基础 URL。默认值为 `http://localhost:11434`。
    *   （可选）如果您的 Ollama 服务器需要身份验证，请输入 API Key。
    *   （高级）Roo 默认为 "ollama" 提供商使用 Ollama 的原生 API。也存在一个兼容 OpenAI 的 `/v1` 处理器，但典型设置不需要它。

---

## 提示和注意事项

*   **资源需求：** 在本地运行大型语言模型可能非常消耗资源。请确保您的计算机满足所选模型的最低要求。
*   **模型选择：** 尝试不同的模型，找到最适合您需求的模型。
*   **离线使用：** 下载模型后，您可以在离线状态下使用该模型运行 Roo Code。
*   **Token 跟踪：** Roo Code 会跟踪通过 Ollama 运行的模型的 token 使用情况，帮助您监控消耗。
*   **Ollama 文档：** 请参考 [Ollama 文档](https://ollama.com/docs) 了解有关安装、配置和使用 Ollama 的更多信息。

---

## 故障排除

### 首次请求时出现内存溢出（OOM）

**症状**
- Roo 的首次请求失败，出现内存溢出错误
- 模型首次加载时 GPU/CPU 内存使用量激增
- 在 Ollama 中手动启动模型后可以正常工作

**原因**
如果没有任何模型实例在运行，Ollama 会按需启动一个。在冷启动期间，它可能分配比预期更大的上下文窗口。更大的上下文窗口会增加内存使用量，可能超过可用的 VRAM 或 RAM。这是 Ollama 的启动行为，不是 Roo Code 的错误。

**解决方法**
1. **预加载模型**
   ```bash
   ollama run &lt;model-name&gt;
   ```
   保持运行，然后从 Roo 发出请求。

2. **固定上下文窗口（`num_ctx`）**
   - 选项 A — 交互式会话，然后保存：
     ```bash
     # 在 `ollama run &lt;base-model&gt;` 内部
     /set parameter num_ctx 32768
     /save &lt;your_model_name&gt;
     ```
   - 选项 B — Modelfile（推荐用于可重复性）：
     ```dockerfile
     FROM &lt;base-model&gt;
     PARAMETER num_ctx 32768
     # 根据您的可用内存调整：
     # 16384 对应 ~8GB VRAM
     # 32768 对应 ~16GB VRAM
     # 65536 对应 ~24GB+ VRAM
     ```
     然后创建模型：
     ```bash
     ollama create &lt;your_model_name&gt; -f Modelfile
     ```

3. **确保模型的上下文窗口已固定**
   使用适当的 `num_ctx` 保存您的 Ollama 模型（通过 `/set` + `/save`，或最好是 Modelfile）。**Roo Code 自动检测并使用模型配置的 `num_ctx`** — Roo Code 的 Ollama 提供商中没有手动上下文大小设置。

4. **使用较小的变体**
   如果 GPU 内存有限，请使用较小的量化版本（例如 q4 而不是 q5）或较小的参数大小（例如 7B/13B 而不是 32B）。

5. **OOM 后重启**
   ```bash
   ollama ps
   ollama stop &lt;model-name&gt;
   ```

**快速检查清单**
- 模型在 Roo 请求之前已运行
- `num_ctx` 已固定（Modelfile 或 `/set` + `/save`）
- 模型已使用适当的 `num_ctx` 保存（Roo 自动使用此设置）
- 模型适合可用的 VRAM/RAM
- 没有遗留的 Ollama 进程