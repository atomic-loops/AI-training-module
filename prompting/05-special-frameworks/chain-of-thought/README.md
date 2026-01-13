# Chain of Thought (CoT) Prompting

## 🎯 Overview

Chain of Thought (CoT) prompting encourages models to show their reasoning process step-by-step, leading to more accurate results on complex problems.

## 📖 What is Chain of Thought?

Chain of Thought is a prompting technique where you ask the model to break down its reasoning into intermediate steps, similar to how humans solve problems.

### Basic Example

```python
# Without CoT
"Solve: A store has 15 apples. They sell 6. How many are left?"

# With CoT
"Solve step by step:
A store has 15 apples. They sell 6. How many are left?

Step 1: Start with initial number of apples
Step 2: Subtract the number sold
Step 3: Calculate the result
Step 4: State the final answer"
```

## 🎯 When to Use CoT

### Best For:
- ✅ Mathematical problems
- ✅ Logical reasoning
- ✅ Multi-step calculations
- ✅ Complex problem-solving
- ✅ Need to verify reasoning

### Not Ideal For:
- ❌ Simple, direct questions
- ❌ Quick lookups
- ❌ Single-step tasks
- ❌ Creative writing

## 📝 CoT Prompting Patterns

### Pattern 1: Explicit Steps

```python
"""
Solve this problem step by step:

Problem: {problem}

Step 1: {what to do first}
Step 2: {what to do second}
Step 3: {what to do third}
...
Final Step: {conclusion}
"""
```

### Pattern 2: Let's Think

```python
"""
Let's think through this step by step:

{problem}

First, we need to...
Then, we should...
Next, we can...
Therefore...
"""
```

### Pattern 3: Show Your Work

```python
"""
Solve this problem and show your work:

{problem}

Show:
1. What information you have
2. What you need to find
3. The steps to solve it
4. The final answer
"""
```

## 💡 Advanced CoT Techniques

### 1. Multi-Step Reasoning

```python
"""
Analyze this code step by step:

Code:
{code}

Step 1: Identify the main purpose
Step 2: Trace the execution flow
Step 3: Identify potential issues
Step 4: Suggest improvements
Step 5: Provide optimized version
"""
```

### 2. Branching Logic

```python
"""
Solve this problem:

{problem}

If condition A:
  - Step 1A
  - Step 2A
  - Conclusion A

Else if condition B:
  - Step 1B
  - Step 2B
  - Conclusion B

Else:
  - Step 1C
  - Step 2C
  - Conclusion C
"""
```

### 3. Verification Steps

```python
"""
Solve and verify:

{problem}

Step 1: Solve the problem
Step 2: Check your answer
Step 3: Verify with alternative method
Step 4: Confirm final answer
"""
```

## 🎨 Real-World Examples

### Example 1: Code Review

```python
"""
Review this code step by step:

{code}

Step 1: Understand what the code does
Step 2: Check for syntax errors
Step 3: Identify logic issues
Step 4: Check for security vulnerabilities
Step 5: Evaluate performance
Step 6: Suggest improvements
Step 7: Provide refactored code
"""
```

### Example 2: Data Analysis

```python
"""
Analyze this dataset step by step:

{data}

Step 1: Load and examine the data
Step 2: Check data quality (missing values, outliers)
Step 3: Calculate summary statistics
Step 4: Identify patterns and trends
Step 5: Create visualizations
Step 6: Draw conclusions
Step 7: Provide recommendations
"""
```

### Example 3: Problem Solving

```python
"""
Solve this system design problem step by step:

Problem: Design a URL shortener

Step 1: Understand requirements
Step 2: Identify constraints
Step 3: Design high-level architecture
Step 4: Design data models
Step 5: Design APIs
Step 6: Handle edge cases
Step 7: Estimate scale
Step 8: Identify bottlenecks
"""
```

## 🔧 CoT Best Practices

### 1. Be Explicit About Steps

```python
# ✅ Good: Clear steps
"Step 1: Parse the input
Step 2: Validate the data
Step 3: Process the request"

# ❌ Avoid: Vague steps
"Think about it and solve"
```

### 2. Number Your Steps

```python
# ✅ Good: Numbered
"Step 1, Step 2, Step 3..."

# ✅ Also good: Lettered
"Step A, Step B, Step C..."
```

### 3. Show Intermediate Results

```python
"""
Calculate: (10 + 5) * 3

Step 1: Calculate 10 + 5 = 15
Step 2: Multiply 15 * 3 = 45
Answer: 45
"""
```

### 4. Use Consistent Format

```python
"""
Step 1: [Action] → [Result]
Step 2: [Action] → [Result]
Step 3: [Action] → [Result]
Final: [Conclusion]
"""
```

## 📊 CoT vs Standard Prompting

| Aspect | Standard | CoT |
|--------|----------|-----|
| Accuracy | Good for simple | Better for complex |
| Transparency | Low | High |
| Debugging | Hard | Easy |
| Speed | Faster | Slightly slower |
| Use Case | Simple tasks | Complex reasoning |

## 🔗 Additional Resources

- [Chain of Thought Paper](https://arxiv.org/abs/2201.11903)
- [CoT Prompting Guide](https://www.promptingguide.ai/techniques/cot)

---

**Related**: [Zero-shot & Few-shot](./zero-shot/README.md) | [Role-based Prompting](./role-based/README.md)

