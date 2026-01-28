# OpenCode 接入 NVIDIA 大模型实施计划

## 项目概述

本项目旨在为 OpenCode 配置 NVIDIA AI Foundation Models，使其能够使用 NVIDIA 提供的大语言模型服务。通过在 `opencode.jsonc` 配置文件中添加 NVIDIA 提供商，我们可以访问 NVIDIA NGC 目录中的各种先进模型。

## 配置说明

### 新增的 NVIDIA 提供商配置

```json
"nvidia": {
  "npm": "@ai-sdk/openai-compatible",
  "api": "https://integrate.api.nvidia.com/v1",
  "name": "NVIDIA AI Foundation Models",
  "env": ["NVIDIA_API_KEY"],
  "models": {
    // 支持的 NVIDIA 模型列表
  }
}
```

### 环境变量设置

需要设置环境变量 `NVIDIA_API_KEY`，其值为从 NVIDIA Developer Portal 获取的 API 密钥：

将以下行添加到 `~/.zshrc` 文件中：
```bash
export NVIDIA_API_KEY="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"
```

然后运行以下命令使更改生效：
```bash
source ~/.zshrc
```

或者重新启动终端。

### 配置文件部署

将完成的 `opencode.jsonc` 文件复制到 `~/.opencode` 目录下并覆盖源文件：

```bash
# 创建目标目录（如果不存在）
mkdir -p ~/.opencode

# 复制配置文件并覆盖原文件
cp /Users/sql/Documents/trae_projects/opencode-local/opencode.jsonc ~/.opencode/
```

### 支持的模型

配置中包含了以下 NVIDIA 支持的模型：

#### Meta Llama 系列
1. **meta/llama-3.1-405b-instruct** - Llama 3.1 405B Instruct
   - 上下文长度：128000
   - 输出限制：4096

2. **meta/llama-3.1-70b-instruct** - Llama 3.1 70B Instruct
   - 上下文长度：128000
   - 输出限制：4096

3. **meta/llama-3.1-8b-instruct** - Llama 3.1 8B Instruct
   - 上下文长度：128000
   - 输出限制：4096

4. **meta/llama-3.3-70b-instruct** - Llama 3.3 70B Instruct
   - 上下文长度：128000
   - 输出限制：4096

5. **meta/llama3-70b-instruct** - Llama 3 70B Instruct
   - 上下文长度：8192
   - 输出限制：4096
   - 定价：输入 $0.59/1M tokens，输出 $0.79/1M tokens

6. **meta/llama3-8b-instruct** - Llama 3 8B Instruct
   - 上下文长度：8192
   - 输出限制：4096
   - 定价：输入 $0.05/1M tokens，输出 $0.08/1M tokens

#### NVIDIA Nemotron 系列
7. **nvidia/nemotron-4-340b-instruct** - Nemotron 4 340B Instruct
   - 上下文长度：8192
   - 输出限制：4096
   - 定价：输入 $0.90/1M tokens，输出 $0.90/1M tokens

8. **nvidia/llama-3.1-nemotron-70b-instruct** - Llama 3.1 Nemotron 70B Instruct
   - 上下文长度：128000
   - 输出限制：4096

9. **nvidia/llama-3.1-nemotron-51b-instruct** - Llama 3.1 Nemotron 51B Instruct
   - 上下文长度：128000
   - 输出限制：4096

10. **nvidia/llama-3.1-nemotron-ultra-253b-v1** - Llama 3.1 Nemotron Ultra 253B v1
    - 上下文长度：128000
    - 输出限制：4096

11. **nvidia/llama-3.3-nemotron-super-49b-v1** - Llama 3.3 Nemotron Super 49B v1
    - 上下文长度：128000
    - 输出限制：4096

12. **nvidia/llama-3.3-nemotron-super-49b-v1.5** - Llama 3.3 Nemotron Super 49B v1.5
    - 上下文长度：128000
    - 输出限制：4096

#### Google Gemma 系列
13. **google/gemma-2-27b-it** - Gemma 2 27B IT
    - 上下文长度：4096
    - 输出限制：4096

14. **google/gemma-2-9b-it** - Gemma 2 9B IT
    - 上下文长度：4096
    - 输出限制：4096

15. **google/gemma-3-12b-it** - Gemma 3 12B IT
    - 上下文长度：8192
    - 输出限制：4096

16. **google/gemma-3-27b-it** - Gemma 3 27B IT
    - 上下文长度：8192
    - 输出限制：4096

17. **google/gemma-3-4b-it** - Gemma 3 4B IT
    - 上下文长度：8192
    - 输出限制：4096

18. **google/gemma-7b** - Gemma 7B
    - 上下文长度：8192
    - 输出限制：4096
    - 定价：输入 $0.05/1M tokens，输出 $0.08/1M tokens

#### Microsoft Phi 系列
19. **microsoft/phi-3-medium-128k-instruct** - Phi-3 Medium 128K Instruct
    - 上下文长度：128000
    - 输出限制：4096

20. **microsoft/phi-3-medium-4k-instruct** - Phi-3 Medium 4K Instruct
    - 上下文长度：4000
    - 输出限制：4096

21. **microsoft/phi-3-mini-128k-instruct** - Phi-3 Mini 128K Instruct
    - 上下文长度：128000
    - 输出限制：4096
    - 定价：输入 $0.05/1M tokens，输出 $0.08/1M tokens

22. **microsoft/phi-3-mini-4k-instruct** - Phi-3 Mini 4K Instruct
    - 上下文长度：4000
    - 输出限制：4096

23. **microsoft/phi-3-small-128k-instruct** - Phi-3 Small 128K Instruct
    - 上下文长度：128000
    - 输出限制：4096

24. **microsoft/phi-3-small-8k-instruct** - Phi-3 Small 8K Instruct
    - 上下文长度：8000
    - 输出限制：4096

25. **microsoft/phi-3-vision-128k-instruct** - Phi-3 Vision 128K Instruct
    - 上下文长度：128000
    - 输出限制：4096

26. **microsoft/phi-3.5-mini-instruct** - Phi-3.5 Mini Instruct
    - 上下文长度：128000
    - 输出限制：4096

27. **microsoft/phi-3.5-moe-instruct** - Phi-3.5 MoE Instruct
    - 上下文长度：128000
    - 输出限制：4096

28. **microsoft/phi-3.5-vision-instruct** - Phi-3.5 Vision Instruct
    - 上下文长度：128000
    - 输出限制：4096

#### Mistral 系列
29. **mistralai/mistral-large** - Mistral Large
    - 上下文长度：32768
    - 输出限制：4096
    - 定价：输入 $2.00/1M tokens，输出 $6.00/1M tokens

30. **mistralai/mistral-large-2-instruct** - Mistral Large 2 Instruct
    - 上下文长度：32768
    - 输出限制：4096

31. **mistralai/mixtral-8x22b-instruct-v0.1** - Mixtral 8x22B Instruct v0.1
    - 上下文长度：65536
    - 输出限制：4096

32. **mistralai/mixtral-8x7b-instruct-v0.1** - Mixtral 8x7B Instruct v0.1
    - 上下文长度：32768
    - 输出限制：4096

#### Qwen 系列
33. **qwen/qwen2.5-coder-32b-instruct** - Qwen2.5 Coder 32B Instruct
    - 上下文长度：32768
    - 输出限制：4096

34. **qwen/qwen3-coder-480b-a35b-instruct** - Qwen3 Coder 480B A35B Instruct
    - 上下文长度：131072
    - 输出限制：4096

#### NVIDIA 专用模型
35. **nvidia/llama3-chatqa-1.5-70b** - Llama3 ChatQA 1.5 70B
    - 上下文长度：8192
    - 输出限制：4096

36. **nvidia/llama3-chatqa-1.5-8b** - Llama3 ChatQA 1.5 8B
    - 上下文长度：8192
    - 输出限制：4096

#### 其他厂商模型
37. **databricks/dbrx-instruct** - DBRX Instruct
    - 上下文长度：32768
    - 输出限制：4096

38. **deepseek-ai/deepseek-coder-6.7b-instruct** - DeepSeek Coder 6.7B Instruct
    - 上下文长度：16384
    - 输出限制：4096

39. **ibm/granite-3.0-8b-instruct** - Granite 3.0 8B Instruct
    - 上下文长度：32000
    - 输出限制：4096

40. **ibm/granite-3.3-8b-instruct** - Granite 3.3 8B Instruct
    - 上下文长度：128000
    - 输出限制：4096

## 使用说明

### 默认模型配置

- 主模型：`nvidia/meta/llama-3.1-70b-instruct`（70B参数的Llama 3.1模型）
- 小模型：`nvidia/microsoft/phi-3-mini-128k-instruct`（高效的Phi-3小型模型）

### API 访问

NVIDIA API 兼容 OpenAI 格式，因此可以使用相同的调用方法。API 端点为：

```
https://integrate.api.nvidia.com/v1/chat/completions
```

## 实施步骤

1. 确保已安装 `@ai-sdk/openai-compatible` 包
2. 在 `~/.zshrc` 中设置 `NVIDIA_API_KEY` 环境变量
3. 重新加载终端配置 (`source ~/.zshrc`)
4. 将 `opencode.jsonc` 复制到 `~/.opencode/` 目录
5. 验证配置文件格式正确
6. 测试模型连接性

## 注意事项

- 需要有效的 NVIDIA API 密钥才能使用这些模型
- 不同模型有不同的定价结构，请根据需求选择合适的模型
- 部分模型可能具有不同的功能特性（如推理、工具调用等）
- 遵守 NVIDIA 的使用条款和配额限制

## 故障排除

如果遇到连接问题，请检查：
- API 密钥是否正确设置
- 网络连接是否正常
- API 端点 URL 是否正确
- 模型 ID 是否拼写正确
- 配置文件是否已正确复制到 `~/.opencode` 目录