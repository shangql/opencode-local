# OpenCode 配置标准格式详解

## 基本配置结构

根据当前的 opencode.jsonc 文件和行业标准，OpenCode 配置通常包含以下主要部分：

### 1. 基础配置项
```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    // 各种模型提供商配置
  },
  "model": "主模型名称",
  "small_model": "小模型名称"
}
```

## 默认模型配置选项

### 当前支持的默认模型类型：

1. **主模型 (model)**
   - 用途：主要推理和复杂任务
   - 当前设置：`"model": "GLM4.7"`

2. **小模型 (small_model)**
   - 用途：轻量级任务和快速响应
   - 当前设置：`"small_model": "MinMax-M2.1"`

### 可扩展的默认模型场景

基于当前配置和最佳实践，可以配置以下场景的默认模型：

```json
{
  // 基础默认模型
  "model": "nvidia/meta/llama-3.1-70b-instruct",
  "small_model": "nvidia/microsoft/phi-3-mini-128k-instruct",
  
  // 可扩展的场景特定模型（示例）
  "reasoning_model": "nvidia/meta/llama-3.1-405b-instruct",
  "vision_model": "nvidia/microsoft/phi-3.5-vision-instruct",
  "coding_model": "nvidia/qwen/qwen2.5-coder-32b-instruct",
  "chat_model": "nvidia/meta/llama-3.1-70b-instruct",
  "analysis_model": "nvidia/mistralai/mistral-large-2-instruct"
}
```

## 当前配置中的可用模型

### 1. Local Qwen 模型 (20个)
- qwen3-max-2026-01-23
- qwen3-vl-plus
- qwen3-coder-plus
- 以及其他17个Qwen系列模型

### 2. NVIDIA 模型 (40个)
- Meta Llama 系列：405B、70B、8B参数模型
- NVIDIA Nemotron 系列：340B、70B、51B参数模型
- Google Gemma 系列：27B、12B、9B、7B、4B参数模型
- Microsoft Phi 系列：各种尺寸模型
- Mistral 系列：Large、Mixtral模型
- Qwen 系列：Coder模型
- 其他厂商模型

### 3. Local Model 配置
- 基础本地模型配置（当前无具体模型）

## 推荐的场景化配置

### 场景1：代码开发
```json
{
  "model": "nvidia/qwen/qwen2.5-coder-32b-instruct",
  "small_model": "nvidia/deepseek-ai/deepseek-coder-6.7b-instruct"
}
```

### 场景2：文档分析
```json
{
  "model": "nvidia/meta/llama-3.1-405b-instruct",
  "small_model": "nvidia/meta/llama-3.1-70b-instruct"
}
```

### 场景3：视觉任务
```json
{
  "model": "nvidia/microsoft/phi-3.5-vision-instruct",
  "small_model": "nvidia/microsoft/phi-3-vision-128k-instruct"
}
```

### 场景4：推理任务
```json
{
  "model": "nvidia/meta/llama-3.1-405b-instruct",
  "small_model": "nvidia/mistralai/mistral-large-2-instruct"
}
```

## 配置最佳实践

1. **根据任务类型选择模型**：
   - 简单问答：使用小模型
   - 复杂推理：使用大模型
   - 代码生成：使用专门的代码模型
   - 视觉任务：使用支持视觉的模型

2. **考虑成本效益**：
   - 免费模型优先（cost.input = 0）
   - 平衡性能和成本

3. **功能匹配**：
   - 检查模型的功能标志（attachment, reasoning, tool_call, temperature）
   - 确保模型支持所需的功能

4. **上下文长度**：
   - 长文本任务选择大上下文模型
   - 短文本任务可选择小上下文模型

## 当前文件中的模型统计

- Local Qwen 模型：20个
- NVIDIA 模型：40个
- 总计：60个可用模型

这些模型可以根据不同的使用场景进行灵活配置和切换。