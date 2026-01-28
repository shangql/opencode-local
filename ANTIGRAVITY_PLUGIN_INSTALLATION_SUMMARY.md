# OpenCode Antigravity Plugin Installation Summary

## Current Status
The `opencode-antigravity-auth` plugin is **already installed** in your system. Here's what's currently configured:

### Location
- Configuration file: `~/.config/opencode/opencode.json`
- Plugin: `opencode-antigravity-auth@latest`

### Available Antigravity Models
The plugin provides access to these advanced models:

#### Google Gemini Models
- `antigravity-gemini-3-pro` - Gemini 3 Pro with thinking capabilities
  - Context: 1,048,576 tokens
  - Output: 65,535 tokens
  - Variants: low/high thinking levels

- `antigravity-gemini-3-flash` - Gemini 3 Flash with thinking capabilities
  - Context: 1,048,576 tokens
  - Output: 65,536 tokens
  - Variants: minimal/low/medium/high thinking levels

#### Anthropic Claude Models
- `antigravity-claude-sonnet-4-5` - Claude Sonnet 4.5
  - Context: 200,000 tokens
  - Output: 64,000 tokens

- `antigravity-claude-sonnet-4-5-thinking` - Claude Sonnet 4.5 with thinking
  - Context: 200,000 tokens
  - Output: 64,000 tokens
  - Variants: low/max thinking budget

- `antigravity-claude-opus-4-5-thinking` - Claude Opus 4.5 with thinking
  - Context: 200,000 tokens
  - Output: 64,000 tokens
  - Variants: low/max thinking budget

### Other Available Models
- `gemini-2.5-flash` - Standard Gemini 2.5 Flash
- `gemini-2.5-pro` - Standard Gemini 2.5 Pro
- `gemini-3-flash-preview` - Preview of Gemini 3 Flash
- `gemini-3-pro-preview` - Preview of Gemini 3 Pro

## Current Default Models Configuration
The current configuration uses ZhipuAI models as defaults:
- Main model: `zhipuai-coding-plan/glm-4.6`
- Small model: `zhipuai-coding-plan/glm-4.5-air`

## Recommended Configuration
I've updated the configuration to use the NVIDIA models we previously set up as defaults while keeping the Antigravity models available:

- Main model: `nvidia/meta/llama-3.1-70b-instruct`
- Small model: `nvidia/microsoft/phi-3-mini-128k-instruct`
- Reasoning model: `nvidia/meta/llama-3.1-405b-instruct`
- Vision model: `nvidia/microsoft/phi-3.5-vision-instruct`
- Coding model: `nvidia/qwen/qwen2.5-coder-32b-instruct`
- Chat model: `nvidia/meta/llama-3.1-70b-instruct`
- Analysis model: `nvidia/mistralai/mistral-large-2-instruct`

## Configuration File Location
- Primary: `~/.config/opencode/opencode.json`
- Alternative: `~/.opencode/opencode.jsonc`

## Additional Configuration
An optional configuration file can be created at `~/.config/opencode/antigravity.json` for advanced settings, but this is not required for basic usage.

## Legal Notice
Please note the legal considerations mentioned in the original plugin documentation:
- This approach may violate Terms of Service of AI model providers
- There's a risk of account suspension or banning
- Use for personal/internal development only
- Not intended for production services