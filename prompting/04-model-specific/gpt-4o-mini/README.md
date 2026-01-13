# GPT-4o-mini Prompting Guide

## 🎯 Overview

GPT-4o-mini is OpenAI's fast and cost-effective model, optimized for speed and efficiency while maintaining good quality.

## 📊 Model Specifications

- **Context Window**: 128K tokens
- **Output Limit**: 16K tokens
- **Best For**: Quick tasks, simple to medium complexity
- **Cost**: Lower than GPT-4o
- **Speed**: Faster than GPT-4o

## 🎯 Optimal Prompting Styles

### 1. Direct and Concise

GPT-4o-mini works best with clear, direct prompts:

```python
# ✅ Good: Direct and clear
"Write a Python function to calculate factorial. Include error handling."

# ❌ Avoid: Overly verbose
"Could you please, if it's not too much trouble, write a Python function..."
```

### 2. Structured Instructions

Use clear structure for better results:

```python
"""
Task: Create a REST API endpoint
Language: Python Flask
Requirements:
- GET /users endpoint
- Return JSON format
- Include error handling
"""
```

### 3. Example-Driven

Provide examples for consistency:

```python
"""
Format: JSON object with 'status' and 'data' fields

Example:
{
  "status": "success",
  "data": {...}
}

Generate similar format for user data.
"""
```

## 💡 Best Practices

### 1. Be Specific

```python
# ✅ Specific
"Write a function that validates email addresses using regex in Python"

# ❌ Vague
"Write something about emails"
```

### 2. Set Constraints Early

```python
"""
Constraints:
- Python 3.9+
- Standard library only
- Type hints required
- Must handle edge cases
"""
```

### 3. Use Step-by-Step for Complex Tasks

```python
"""
Step 1: Parse the input
Step 2: Validate the data
Step 3: Process the request
Step 4: Return formatted response
"""
```

## 🚫 What to Avoid

### 1. Overly Complex Prompts

Keep it simple - GPT-4o-mini excels at straightforward tasks.

### 2. Excessive Context

While it supports 128K context, be concise for better speed.

### 3. Ambiguous Instructions

Be explicit about what you want.

## 📝 Code Generation Tips

### Effective Code Prompts

```python
"""
Write a Python function with:
- Function name: calculate_total
- Parameters: items (list of dicts with 'price' and 'quantity')
- Returns: float (total cost)
- Includes: Type hints, docstring, error handling
"""
```

### Testing Prompts

```python
"""
Write unit tests for this function:
{function_code}

Requirements:
- Use pytest
- Cover edge cases
- Test error conditions
- Minimum 5 test cases
"""
```

## 🎨 Use Cases

### Best For:
- ✅ Quick code snippets
- ✅ Simple data processing
- ✅ Basic analysis
- ✅ Text formatting
- ✅ Simple Q&A

### Not Ideal For:
- ❌ Complex multi-step reasoning
- ❌ Very long outputs (>16K tokens)
- ❌ Highly creative writing
- ❌ Complex mathematical proofs

## 📋 Example Prompts

### Code Generation

```python
"""
Create a Python class 'User' with:
- Attributes: id, name, email
- Methods: __init__, __str__, to_dict
- Validation: email format check
- Type hints throughout
"""
```

### Data Analysis

```python
"""
Analyze this dataset:
{data}

Provide:
1. Summary statistics
2. Key insights (3-5 points)
3. One recommendation
"""
```

### Text Processing

```python
"""
Format this text:
- Remove extra whitespace
- Capitalize first letter of sentences
- Fix common typos
- Return cleaned text
"""
```

## 🔧 Advanced Techniques

### 1. Few-Shot Learning

```python
"""
Example 1:
Input: "Hello world"
Output: "HELLO WORLD"

Example 2:
Input: "Python programming"
Output: "PYTHON PROGRAMMING"

Now convert: "Data science"
"""
```

### 2. Chain of Thought

```python
"""
Solve step by step:
Problem: Calculate 15% tip on $50 bill

Step 1: Identify the base amount
Step 2: Calculate 15% of base
Step 3: Add tip to base
Step 4: State final answer
"""
```

### 3. Output Formatting

```python
"""
Return output as JSON:
{
  "result": "...",
  "explanation": "...",
  "code": "..."
}
"""
```

## 📊 Performance Tips

1. **Keep prompts concise** for faster responses
2. **Use structured output** when possible
3. **Set temperature to 0** for deterministic results
4. **Limit output length** to stay within 16K tokens

## 🔗 Additional Resources

- [OpenAI GPT-4o-mini Documentation](https://platform.openai.com/docs/models/gpt-4o-mini)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)

---

**Related**: [GPT-4o Guide](./gpt-4o/README.md) | [GPT-4 Turbo Guide](./gpt-4-turbo/README.md)

