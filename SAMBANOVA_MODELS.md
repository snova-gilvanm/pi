# SambaNova Cloud Models in Pi

All 6 SambaNova cloud models are now available in Pi! Choose the right model for your use case.

## 📊 Available Models

### Production Models

#### 1. **Meta Llama 3.3 70B Instruct**
```bash
pi --model Meta-Llama-3.3-70B-Instruct
```
- **Provider**: Meta
- **Context Window**: 128K tokens
- **Max Output**: 12.8K tokens
- **Thinking/Reasoning**: ❌ No
- **Image Support**: ❌ No
- **Best For**: Fast, high-quality text generation, general purpose coding
- **Inference Speed**: ⚡⚡⚡ Very Fast (70B optimized)

#### 2. **MiniMax M2.7**
```bash
pi --model MiniMax-M2.7
```
- **Provider**: MiniMax
- **Context Window**: 192K tokens ⭐ (LARGEST)
- **Max Output**: 19.2K tokens
- **Thinking/Reasoning**: ❌ No
- **Image Support**: ❌ No
- **Best For**: Very long document analysis, context-heavy tasks, code review of large files
- **Inference Speed**: ⚡⚡ Fast (optimized for long context)

#### 3. **OpenAI GPT OSS 120B**
```bash
pi --model gpt-oss-120b
```
- **Provider**: OpenAI
- **Context Window**: 128K tokens
- **Max Output**: 12.8K tokens
- **Thinking/Reasoning**: ✅ Yes
- **Image Support**: ❌ No
- **Best For**: Complex reasoning, logic puzzles, step-by-step problem solving
- **Inference Speed**: ⚡⚡ Moderate (reasoning adds latency)

#### 4. **DeepSeek V3.1**
```bash
pi --model DeepSeek-V3.1
```
- **Provider**: DeepSeek
- **Context Window**: 128K tokens
- **Max Output**: 12.8K tokens
- **Thinking/Reasoning**: ✅ Yes (Extended Thinking)
- **Image Support**: ❌ No
- **Best For**: Complex coding tasks, mathematical reasoning, detailed analysis
- **Inference Speed**: ⚡⚡ Moderate (reasoning enabled)
- **Notes**: Enterprise-focused model with strong reasoning capabilities

---

### Preview Models

#### 5. **DeepSeek V3.2 (Preview)**
```bash
pi --model DeepSeek-V3.2
```
- **Provider**: DeepSeek
- **Context Window**: 32K tokens
- **Max Output**: 3.2K tokens
- **Thinking/Reasoning**: ✅ Yes (Extended Thinking)
- **Image Support**: ❌ No
- **Best For**: Quick reasoning tasks, code snippets (within 32K context)
- **Inference Speed**: ⚡⚡⚡ Fastest (smaller model)
- **Status**: 🔔 Preview - May change before general availability
- **Warning**: Smallest context window - suitable for smaller inputs only

#### 6. **Google Gemma 4 31B Instruct (Preview)**
```bash
pi --model gemma-4-31B-it
```
- **Provider**: Google
- **Context Window**: 128K tokens
- **Max Output**: 12.8K tokens
- **Thinking/Reasoning**: ❌ No
- **Image Support**: ✅ Yes (Text & Image Input)
- **Best For**: Multimodal tasks, analyzing code screenshots, image-based documentation
- **Inference Speed**: ⚡⚡⚡ Very Fast
- **Status**: 🔔 Preview - May change before general availability
- **Unique Feature**: Only model with vision/image support!

---

## 🎯 Model Selection Guide

### By Use Case

| Use Case | Best Model | Reason |
|----------|-----------|--------|
| **General Code Generation** | Meta Llama 3.3 70B | Fast, reliable, balanced |
| **Long Documents/Analysis** | MiniMax M2.7 | 192K context, handles huge files |
| **Complex Math/Logic** | DeepSeek V3.1 or GPT OSS 120B | Extended thinking/reasoning |
| **Quick Tasks** | DeepSeek V3.2 | Fastest, good reasoning |
| **Image/Vision Analysis** | Gemma 4 31B | Only multimodal option |
| **Production Use** | Meta Llama 3.3 70B or MiniMax M2.7 | Stable, proven |

### By Priority

**⚡ Speed**: DeepSeek V3.2 > Gemma 4 31B > Meta Llama 3.3 > MiniMax M2.7 > DeepSeek V3.1

**🧠 Reasoning**: DeepSeek V3.1 > GPT OSS 120B (tied) > DeepSeek V3.2

**📝 Context Window**: MiniMax M2.7 (192K) > Others (128K) > DeepSeek V3.2 (32K)

**🖼️ Multimodal**: Gemma 4 31B (only option)

**✅ Production Ready**: Meta Llama 3.3, MiniMax M2.7, GPT OSS 120B, DeepSeek V3.1

---

## 💡 Usage Examples

### Interactive Mode with Model Selection
```bash
export SAMBANOVA_API_KEY="your-key"
./pi-test.sh
# Then in Pi:
/model
# Select from the list of SambaNova models
```

### Command Line with Specific Model
```bash
# Fast model for quick tasks
pi --model Meta-Llama-3.3-70B-Instruct "Explain this code"

# Large context for big files
pi --model MiniMax-M2.7 --model-override "Analyze this 100K token document"

# Reasoning for complex problems
pi --model DeepSeek-V3.1 "Solve this logic puzzle"

# Vision for image analysis
pi --model gemma-4-31B-it "What's in this screenshot?"
```

### Batch Processing
```bash
# Use smaller, faster model
for file in *.py; do
  echo "Reviewing $file"
  pi --model Meta-Llama-3.3-70B-Instruct --no-session < "$file"
done
```

---

## 📈 Performance Characteristics

### Throughput (tokens/sec - estimated)
| Model | Estimate | Notes |
|-------|----------|-------|
| DeepSeek V3.2 | ~200-300 | Smallest, fastest |
| Gemma 4 31B | ~150-200 | Vision processing overhead |
| Meta Llama 3.3 | ~100-150 | Balanced |
| GPT OSS 120B | ~80-120 | Reasoning adds latency |
| DeepSeek V3.1 | ~80-120 | Extended thinking |
| MiniMax M2.7 | ~60-100 | Optimized for large context |

### Quality Ranking (subjective)
**Reasoning/Logic**: DeepSeek V3.1 > GPT OSS 120B > Others

**Coding**: Meta Llama 3.3 ≈ DeepSeek V3.1 > GPT OSS 120B > Gemma 4

**Context Handling**: MiniMax M2.7 > Others (thanks to 192K window)

**Instruction Following**: Meta Llama 3.3 > Gemma 4 > Others

---

## 🔄 Model Comparison Table

| Feature | Meta Llama 3.3 | MiniMax M2.7 | GPT OSS 120B | DeepSeek V3.1 | DeepSeek V3.2 | Gemma 4 |
|---------|---|---|---|---|---|---|
| **Context** | 128K | **192K** | 128K | 128K | 32K | 128K |
| **Reasoning** | ❌ | ❌ | ✅ | ✅ | ✅ | ❌ |
| **Vision** | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| **Speed** | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| **Status** | ✅ Production | ✅ Production | ✅ Production | ✅ Production | 🔔 Preview | 🔔 Preview |

---

## ⚙️ Configuration

### Default Model
Currently set to `Meta-Llama-3.3-70B-Instruct` (good general-purpose default).

To change the default:
```bash
# Edit packages/coding-agent/src/core/model-resolver.ts
sambanova: "MiniMax-M2.7", # Change this to your preferred model

# Then rebuild
npm run build
```

### Pricing
All SambaNova models show $0 cost (placeholder). To add pricing:

Edit `packages/ai/scripts/generate-models.ts` in the `sambanovaModels` array:
```typescript
{
  id: "Meta-Llama-3.3-70B-Instruct",
  // ... other fields ...
  costPerMillionInputTokens: 0.25,  // ← Add actual pricing
  costPerMillionOutputTokens: 0.75,
}
```

Then rebuild: `npm run build`

---

## 📚 Detailed Documentation

For more information on these models, see:
- **SambaNova Cloud Models**: https://docs.sambanova.ai/docs/en/models/sambacloud-models
- **SambaNova API Docs**: https://docs.sambanovasystems.com
- **Pi Documentation**: https://pi.dev/docs

---

## 🆘 Troubleshooting

### Model not working
```bash
# Verify your API key
echo $SAMBANOVA_API_KEY

# Test connection
./pi-test.sh --model Meta-Llama-3.3-70B-Instruct --mode text --no-session
```

### Input too long
If you get a context window error:
- **DeepSeek V3.2**: Limited to 32K - try a longer-context model
- **Others**: Limited to 128K - try MiniMax M2.7 (192K)

### Vision not working
Only **gemma-4-31B-it** supports images. For other models, text descriptions of images work better.

---

## 🎁 What's Next

1. **Pick your favorite model** - Try each one with a test request
2. **Set as default** (optional) - Change the default model if preferred
3. **Add pricing** (optional) - Update costs when available from SambaNova
4. **Explore features** - Use multimodal Gemma for images, or large MiniMax for documents

---

**Build Status**: ✅ All 6 models integrated and working

**Ready to use**: `pi --model <model-name>` or `/login sambanova` then `/model`

**Questions?** Check https://pi.dev or join the Pi Discord: https://discord.com/invite/3cU7Bz4UPx
