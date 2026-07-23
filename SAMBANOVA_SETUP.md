# Installing Pi with SambaNova Provider Support

This guide covers installing Pi with SambaNova as a built-in provider.

## What Was Added

SambaNova is now a built-in provider in the Pi monorepo with:
- **Provider implementation**: `packages/ai/src/providers/sambanova.ts`
- **Model data**: `packages/ai/src/providers/data/sambanova.json` (currently placeholder models)
- **Type integration**: Added to `KnownProvider` union in `packages/ai/src/types.ts`
- **Registration**: Added to `packages/ai/src/providers/all.ts` and `register-builtins.ts`
- **CLI support**: Environment variable docs, model resolver defaults, provider documentation
- **Documentation**: Updated in `packages/coding-agent/docs/providers.md` and README

## Step 1: Update Model Configuration

The current `sambanova.json` has placeholder models. You need to update it with your actual SambaNova models.

Edit `/packages/ai/src/providers/data/sambanova.json` and add your real models. Each model needs:

```json
{
  "openai-completions": {
    "your-model-id": {
      "id": "your-model-id",
      "name": "Your Model Name",
      "api": "openai-completions",
      "provider": "sambanova",
      "baseUrl": "https://api.sambanovasystems.com/v1",
      "reasoning": false,
      "input": ["text"],
      "cost": {
        "input": 0.01,
        "output": 0.05,
        "cacheRead": 0,
        "cacheWrite": 0
      },
      "contextWindow": 131072,
      "maxTokens": 4096
    }
  }
}
```

**Key fields:**
- `id`: The model ID you'll use in `/model` command or `--model` CLI arg
- `name`: Display name shown in the UI
- `contextWindow`: Maximum context length in tokens
- `cost`: Pricing per 1M tokens (input/output), or 0 if not available
- `reasoning`: Set to `true` if model supports extended thinking

## Step 2: Build Pi from Source

```bash
npm install --ignore-scripts
npm run build
```

This generates the model catalogs and builds all packages.

## Step 3: Set Your API Key

Choose one of these methods:

### Option A: Environment Variable (Recommended for Development)
```bash
export SAMBANOVA_API_KEY="your-api-key-here"
pi
```

### Option B: Using `/login` in Pi
```bash
pi
# Then in interactive mode:
/login
# Select SambaNova from the provider list
# Paste your API key when prompted
```

The API key is stored in `~/.pi/agent/auth.json` and automatically refreshed.

### Option C: Store in `auth.json` Directly
Edit `~/.pi/agent/auth.json`:
```json
{
  "sambanova": {
    "type": "api_key",
    "key": "your-api-key-here"
  }
}
```

## Step 4: Configure Default Model (Optional)

If you want to change the default model from `sambanova-large`:

Edit `packages/coding-agent/src/core/model-resolver.ts`:
```typescript
export const defaultModelPerProvider: Record<KnownProvider, string> = {
  // ...
  sambanova: "your-preferred-model-id",
  // ...
};
```

Then rebuild: `npm run build`

## Step 5: Verify Installation

Run Pi and select a SambaNova model:

```bash
pi
# In interactive mode:
/model
# Select a SambaNova model from the list
```

Or specify it directly:
```bash
pi --model sambanova-large
```

## Testing

### Quick Test
```bash
export SAMBANOVA_API_KEY="your-key"
echo "Hello world" | pi --model sambanova-large --mode text --no-session
```

### Interactive Mode
```bash
export SAMBANOVA_API_KEY="your-key"
pi --model sambanova-large
# Then ask the agent a question
```

### List All SambaNova Models
```bash
pi --list-models sambanova
```

## Customization

### Using a Custom API Endpoint

Edit `packages/ai/src/providers/sambanova.ts`:
```typescript
export function sambanovaProvider(): Provider<"openai-completions"> {
  return createProvider({
    id: "sambanova",
    name: "SambaNova",
    baseUrl: "https://your-custom-endpoint.com/v1",  // ← Change this
    auth: { apiKey: envApiKeyAuth("SambaNova API key", ["SAMBANOVA_API_KEY"]) },
    models: Object.values(SAMBANOVA_MODELS),
    api: openAICompletionsApi(),
  });
}
```

Then rebuild: `npm run build`

### Using a Different API Format

If SambaNova's API is not OpenAI-compatible, you may need a custom API implementation. See `packages/ai/src/api/` for examples. This is more complex - reach out on Discord if needed.

## Troubleshooting

### Models not appearing
1. Verify `sambanova.json` is valid JSON: `node -e "console.log(require('./packages/ai/src/providers/data/sambanova.json'))"`
2. Rebuild models: `npm run build` (includes `npm run generate-models`)
3. Check that `SAMBANOVA_MODELS` export exists in `packages/ai/src/providers/sambanova.models.ts`

### API key not found
1. Check env var: `echo $SAMBANOVA_API_KEY`
2. Check `auth.json`: `cat ~/.pi/agent/auth.json | jq .sambanova`
3. Run `/login sambanova` to re-authenticate

### Connection errors
1. Verify base URL is correct and accessible: `curl https://api.sambanovasystems.com/v1/models -H "Authorization: Bearer YOUR_KEY"`
2. Check firewall/proxy settings
3. Verify API key is valid and not expired

### "Model not supported" error
1. Ensure model ID in `sambanova.json` exactly matches what SambaNova API returns
2. Verify the model supports tool calling (required for agentic workflows)

## Contributing Back

If you improve the SambaNova provider or add features, consider contributing to the Pi project:

1. Fork https://github.com/earendil-works/pi
2. Make your changes
3. Run `npm run check && ./test.sh` to verify
4. Open a PR with a clear description

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## Next Steps

- **Configure extensions**: Add custom tools, skills, or themes in `~/.pi/agent/`
- **Learn Pi commands**: Run `pi --help` or `/hotkeys` in interactive mode
- **Explore examples**: Check `packages/coding-agent/examples/` for extension templates
- **Read docs**: See `packages/coding-agent/docs/` for detailed guides

## API Compatibility

SambaNova uses OpenAI-compatible format. The current implementation uses:
- **API**: `openai-completions` (streaming text/tool-call format)
- **Auth**: Bearer token via `SAMBANOVA_API_KEY` environment variable
- **Endpoint**: `https://api.sambanovasystems.com/v1` (configurable)

If SambaNova's API changes format, you may need to implement a custom provider or API handler.

## Resources

- Pi Project: https://pi.dev
- Pi GitHub: https://github.com/earendil-works/pi
- Pi Discord: https://discord.com/invite/3cU7Bz4UPx
- SambaNova API Docs: [Add link to your API documentation]

---

**Questions?** Join the Pi Discord or check the project documentation.
