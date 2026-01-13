# Module 4: Model-Specific Prompting

## 🎯 Learning Objectives

By the end of this module, you will understand:
- How different models interpret prompts
- Model-specific optimizations
- Best practices for each model family
- When to use which model
- Model-specific prompting techniques

## 🚀 Getting Started

> **💡 Recommendation**: If you're new to model-specific prompting, **start with the [GPT-4o-mini guide](./gpt-4o-mini/README.md)**. It's fast, cost-effective, and perfect for learning the fundamentals. Once comfortable, explore other models based on your specific needs.

## 📚 Available Model Guides

This module contains detailed guides for specific models:

### OpenAI Models
- **[GPT-4o-mini](./gpt-4o-mini/README.md) - Fast, cost-effective model** ⭐ *Start here!*
- [GPT-4o](./gpt-4o/README.md) - Advanced multimodal model
- [GPT-4 Turbo](./gpt-4-turbo/README.md) - High-performance model

### Anthropic Models
- [Claude 3.5 Sonnet](./claude-3-5-sonnet/README.md) - Balanced performance
- [Claude 3 Opus](./claude-3-opus/README.md) - Most capable model

### Google Models
- [Gemini Pro](./gemini-pro/README.md) - Google's advanced multimodal model

### Open Source Models
- [Llama 3](./llama-3/README.md) - Meta's open-source model
- [Mixtral](./mixtral/README.md) - Mixture of experts model

## 🔍 Model Comparison

### Key Differences

| Model | Strengths | Best For | Context Window |
|-------|-----------|----------|----------------|
| GPT-4o-mini | Speed, Cost | Quick tasks, Simple prompts | 128K |
| GPT-4o | Multimodal, Quality | Complex tasks, Images | 128K |
| GPT-4 Turbo | Performance | Large tasks, Code | 128K |
| Claude 3.5 Sonnet | Balance | General purpose | 200K |
| Claude 3 Opus | Quality | Complex reasoning | 200K |
| Gemini Pro | Multimodal | Google ecosystem | 128K |
| Llama 3 | Open source | Self-hosting | 128K |
| Mixtral | Efficiency | Specialized tasks | 32K |

## 🎯 General Model-Specific Tips

### 1. Context Window Awareness

- **Small context (32K)**: Be concise, remove unnecessary text
- **Large context (200K)**: Can include extensive examples and context

### 2. Token Limits

- **Output limits**: Some models have strict output limits
- **Input optimization**: Remove redundant information

### 3. Model Capabilities

- **Multimodal**: GPT-4o, Gemini can process images
- **Code**: GPT-4 Turbo, Claude excel at code
- **Reasoning**: Claude 3 Opus for complex reasoning

### 4. Temperature Settings

- **Low (0-0.3)**: Deterministic, factual responses
- **Medium (0.5-0.7)**: Balanced creativity and accuracy
- **High (0.8-1.0)**: Creative, varied responses

## 📋 Module 4 Exercises

### Exercise 1: Model Selection
1. Create 5 different tasks
2. Select the best model for each
3. Justify your choices
4. Test with actual models

### Exercise 2: Prompt Adaptation
1. Write a generic prompt
2. Adapt it for 3 different models
3. Compare results
4. Document differences

### Exercise 3: Model Comparison
1. Use the same prompt with 2-3 models
2. Compare outputs
3. Identify strengths/weaknesses
4. Create model-specific optimizations

## 🔗 Additional Resources

- [OpenAI Model Documentation](https://platform.openai.com/docs/models)
- [Anthropic Model Guide](https://docs.anthropic.com/claude/docs/models-overview)
- [Model Comparison Tools](https://www.promptingguide.ai/models)

## ✅ Module 4 Checklist

Before moving to Module 5, ensure you can:

- [ ] Understand model-specific differences
- [ ] Select appropriate models for tasks
- [ ] Adapt prompts for different models
- [ ] Optimize for model capabilities
- [ ] Use model-specific features effectively

---

**Next Steps**: Explore specific model guides or proceed to [Module 5: Special Frameworks](../05-special-frameworks/README.md)

