# ✅ SambaNova Cloud Models - Full Integration Complete

All **6 SambaNova Cloud models** from the official documentation are now integrated and ready to use in Pi!

## 🎯 What's Available

```
provider   model                        context  max-out  thinking  images
sambanova  DeepSeek-V3.1                128K     12.8K    yes       no    
sambanova  DeepSeek-V3.2                32K      3.2K     yes       no    
sambanova  gemma-4-31B-it               128K     12.8K    no        yes   
sambanova  gpt-oss-120b                 128K     12.8K    yes       no    
sambanova  Meta-Llama-3.3-70B-Instruct  128K     12.8K    no        no    
sambanova  MiniMax-M2.7                 192K     19.2K    no        no    
```

### Quick Facts
- **Total Models**: 6 (4 production + 2 preview)
- **Largest Context**: MiniMax M2.7 (192K tokens)
- **Only Vision Model**: Gemma 4 31B (text + image input)
- **Reasoning Models**: DeepSeek V3.1, V3.2, GPT OSS 120B (extended thinking)
- **Default Model**: Meta Llama 3.3 70B (balanced, fast, production-ready)

## 🚀 Quick Start

### List All Models
```bash
./pi-test.sh --list-models sambanova
```

### Use Default Model (Meta Llama 3.3)
```bash
export SAMBANOVA_API_KEY="your-key"
./pi-test.sh
```

### Use Specific Model
```bash
# Large context for big files
pi --model MiniMax-M2.7

# Reasoning for complex tasks
pi --model DeepSeek-V3.1

# Vision for image analysis
pi --model gemma-4-31B-it

# Production-ready, fast
pi --model Meta-Llama-3.3-70B-Instruct
```

## 📋 Model Details

### Production Models (Stable)

#### Meta Llama 3.3 70B Instruct ⭐ DEFAULT
- **ID**: `Meta-Llama-3.3-70B-Instruct`
- **Context**: 128K tokens
- **Speed**: ⚡⚡⚡ Very fast
- **Reasoning**: No
- **Best For**: General-purpose code, balance of speed and quality
- **Status**: ✅ Production

#### MiniMax M2.7 (Largest Context)
- **ID**: `MiniMax-M2.7`
- **Context**: 192K tokens (largest!)
- **Speed**: ⚡⚡ Moderate
- **Best For**: Very long documents, entire codebases, extensive analysis
- **Status**: ✅ Production

#### OpenAI GPT OSS 120B (Strong Reasoning)
- **ID**: `gpt-oss-120b`
- **Context**: 128K tokens
- **Speed**: ⚡⚡ Moderate
- **Reasoning**: ✅ Extended thinking
- **Best For**: Complex logic, mathematical problems, deep analysis
- **Status**: ✅ Production

#### DeepSeek V3.1 (Enterprise)
- **ID**: `DeepSeek-V3.1`
- **Context**: 128K tokens
- **Speed**: ⚡⚡ Moderate
- **Reasoning**: ✅ Extended thinking
- **Best For**: Complex coding, detailed reasoning
- **Status**: ✅ Production

### Preview Models (Experimental)

#### DeepSeek V3.2 (Fastest)
- **ID**: `DeepSeek-V3.2`
- **Context**: 32K tokens
- **Speed**: ⚡⚡⚡ Fastest
- **Reasoning**: ✅ Extended thinking
- **Best For**: Quick reasoning tasks, smaller inputs
- **Status**: 🔔 Preview

#### Gemma 4 31B (Vision Support) 🖼️
- **ID**: `gemma-4-31B-it`
- **Context**: 128K tokens
- **Speed**: ⚡⚡⚡ Very fast
- **Vision**: ✅ Text + image input
- **Best For**: Screenshots, diagrams, image-based documentation
- **Status**: 🔔 Preview
- **Unique**: Only multimodal model!

## 🎯 Selection Guide

| Need | Model | Why |
|------|-------|-----|
| **Default choice** | Meta Llama 3.3 | Balanced, fast, production-ready |
| **Huge documents** | MiniMax M2.7 | 192K context handles anything |
| **Hard problems** | DeepSeek V3.1 | Excellent reasoning |
| **Quick answers** | DeepSeek V3.2 | Fastest model |
| **Analyze images** | Gemma 4 31B | Only vision option |
| **Logic puzzles** | GPT OSS 120B | Strong reasoning |

## 📝 Usage Examples

### Interactive Mode
```bash
export SAMBANOVA_API_KEY="your-api-key"
./pi-test.sh
# In Pi, type: /model
# Select from SambaNova options
```

### CLI with Model
```bash
# Quick task with default
pi "Explain this Python function"

# Large file with big context
pi --model MiniMax-M2.7 @large_file.py

# Reasoning task
pi --model DeepSeek-V3.1 "Solve this equation"

# Image analysis
pi --model gemma-4-31B-it "What's in this screenshot?"
```

### Batch Processing
```bash
# Review all Python files quickly
for f in src/*.py; do
  pi --no-session --model Meta-Llama-3.3-70B-Instruct < "$f"
done
```

## 📊 Performance Comparison

### Context Window
```
MiniMax M2.7:    192K ████████████████████ LARGEST
Others (5):      128K ████████████ (same)
DeepSeek V3.2:    32K ████ smallest
```

### Speed (estimated throughput)
```
DeepSeek V3.2:   ▓▓▓ fastest
Gemma 4 31B:     ▓▓▓ very fast
Meta Llama 3.3:  ▓▓ fast
GPT OSS 120B:    ▓▓ moderate
DeepSeek V3.1:   ▓▓ moderate
MiniMax M2.7:    ▓  slowest (due to large context)
```

### Reasoning Capability
```
DeepSeek V3.1:   ▓▓▓ excellent
GPT OSS 120B:    ▓▓▓ excellent
DeepSeek V3.2:   ▓▓ good
Others (3):      ░░ none (text generation focus)
```

## ⚙️ Configuration

### Change Default Model
Edit `packages/coding-agent/src/core/model-resolver.ts`:
```typescript
sambanova: "MiniMax-M2.7", // or any other model ID
```
Then: `npm run build`

### Add Pricing (When Available)
Edit `packages/ai/scripts/generate-models.ts` in the sambanovaModels section:
```typescript
{
  id: "Meta-Llama-3.3-70B-Instruct",
  // Add real pricing when available:
  costPerMillionInputTokens: 0.0X,
  costPerMillionOutputTokens: 0.0X,
}
```

### Custom Base URL
Edit `packages/ai/src/providers/sambanova.ts`:
```typescript
baseUrl: "https://your-custom-endpoint/v1",
```

## 🔐 Authentication

### Using Environment Variable (Development)
```bash
export SAMBANOVA_API_KEY="your-key"
pi --model Meta-Llama-3.3-70B-Instruct
```

### Using /login (Interactive)
```bash
pi
/login sambanova
# Follow prompts to authenticate
# Key stored in ~/.pi/agent/auth.json
```

### Direct File (Advanced)
```bash
cat ~/.pi/agent/auth.json
# Should contain:
# {
#   "sambanova": {
#     "type": "api_key",
#     "key": "your-key-here"
#   }
# }
```

## 📚 Model Documentation

For detailed information:
- **SambaNova Cloud Models**: https://docs.sambanova.ai/docs/en/models/sambacloud-models
- **Complete Model Guide**: See `SAMBANOVA_MODELS.md` (in this repo)
- **Setup Instructions**: See `SAMBANOVA_SETUP.md`

## ✨ Features

- ✅ **All 6 models available** via `pi --model <name>`
- ✅ **Vision support** with Gemma 4 31B (image input)
- ✅ **Reasoning models** with extended thinking capability
- ✅ **Large context** with MiniMax M2.7 (192K)
- ✅ **Production-ready** defaults
- ✅ **Cost tracking** when pricing is added
- ✅ **Full CLI integration** `/login`, `/model`, `--model` flag
- ✅ **Environment variable** authentication
- ✅ **Auth file** persistence

## 🛠️ Technical Details

| Aspect | Details |
|--------|---------|
| **API Format** | OpenAI-compatible (`openai-completions`) |
| **Authentication** | Bearer token via `SAMBANOVA_API_KEY` |
| **Base URL** | https://api.sambanovasystems.com/v1 |
| **Models Count** | 6 (4 production + 2 preview) |
| **Vision Support** | Gemma 4 31B only |
| **Reasoning Support** | DeepSeek V3.1, V3.2, GPT OSS 120B |
| **Max Context** | MiniMax M2.7 (192K tokens) |
| **Max Output** | 10% of context window (conservative) |

## 📋 Build Status

```
✅ Type checking: PASSED
✅ Linting: PASSED
✅ Model generation: PASSED (6 models)
✅ Build: PASSED
✅ Model listing: PASSED
```

**Total tool-capable models**: 1114 (including 6 SambaNova)

## 🎁 What's Next

1. **Test each model** - Try one or two to understand differences
2. **Pick your default** - Edit model-resolver.ts if you prefer a different default
3. **Add pricing** - Update costs when available from SambaNova
4. **Use in production** - Integrate into your workflows

## 💬 Support

- **Questions about Pi**: https://pi.dev | Discord: https://discord.com/invite/3cU7Bz4UPx
- **SambaNova Documentation**: https://docs.sambanovasystems.com
- **Model Information**: See included `SAMBANOVA_MODELS.md`

---

**Status**: ✅ **Complete and Ready to Use**

**Get started**: 
```bash
export SAMBANOVA_API_KEY="your-key"
pi --model Meta-Llama-3.3-70B-Instruct "What's 2+2?"
```

Enjoy using all 6 SambaNova Cloud models in Pi! 🚀
