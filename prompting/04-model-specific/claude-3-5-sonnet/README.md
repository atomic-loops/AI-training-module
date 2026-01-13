# Claude 3.5 Sonnet Prompting Guide

## 🎯 Overview

Claude 3.5 Sonnet is Anthropic's balanced model, offering excellent performance across a wide range of tasks with a large context window.

## 📊 Model Specifications

- **Context Window**: 200K tokens
- **Output Limit**: 8K tokens
- **Best For**: General purpose, long documents, balanced performance
- **Cost**: Moderate
- **Speed**: Good

## 🎯 Optimal Prompting Styles

### 1. Long Context Prompts

Claude excels with large context windows:

```python
"""
You have access to this entire document:
{document}

Analyze and provide:
1. Key themes
2. Important points
3. Recommendations
"""
```

### 2. Conversational Style

```python
"""
Let's work through this together:

{problem}

I'd like you to:
- Think through the approach
- Consider alternatives
- Provide your reasoning
- Give recommendations
"""
```

### 3. Detailed Analysis

```python
"""
Perform a comprehensive analysis:

Topic: {topic}

Include:
- Background context
- Current state
- Key factors
- Potential solutions
- Recommendations
"""
```

## 💡 Best Practices

1. **Use the large context window** for extensive documents
2. **Be conversational** - Claude responds well to natural language
3. **Request reasoning** - Claude excels at explaining its thinking
4. **Ask for alternatives** - Claude can provide multiple perspectives

## 🎨 Use Cases

### Best For:
- ✅ Long document analysis
- ✅ Complex reasoning
- ✅ Conversational interactions
- ✅ Multi-step problem solving
- ✅ Detailed explanations

## 📋 Example Prompts

### Document Analysis

```python
"""
Analyze this 50-page document:
{document}

Provide:
1. Executive summary
2. Key findings
3. Important quotes
4. Action items
"""
```

### Reasoning Tasks

```python
"""
Think through this problem step by step:

{problem}

Show your reasoning at each step and explain your conclusions.
"""
```


**Related**: [Claude 3 Opus Guide](./claude-3-opus/README.md) | [Model Comparison](../README.md)

