# Zero-shot and Few-shot Prompting

## 🎯 Overview

Zero-shot and few-shot prompting are techniques that leverage the model's ability to learn from examples provided in the prompt itself.

## 📖 What is Zero-shot Prompting?

Zero-shot prompting means giving the model a task without any examples, relying on its pre-trained knowledge.

### Basic Example

```python
# Zero-shot: No examples provided
"Translate this to French: Hello, how are you?"
```

## 📖 What is Few-shot Prompting?

Few-shot prompting provides a few examples (typically 2-5) to show the model the desired pattern or format.

### Basic Example

```python
# Few-shot: Examples provided
"""
Example 1:
Input: "Hello"
Output: "Bonjour"

Example 2:
Input: "Good morning"
Output: "Bonjour"

Now translate: "Good evening"
"""
```

## 🎯 Zero-shot Prompting

### When to Use

✅ **Use zero-shot when:**
- Simple, straightforward tasks
- Model has strong pre-training on the task
- Quick responses needed
- No specific format required

### Examples

```python
# Classification
"Classify this text as positive, negative, or neutral: {text}"

# Generation
"Write a Python function to reverse a string"

# Analysis
"Summarize this article: {article}"

# Translation
"Translate to Spanish: {text}"
```

### Best Practices

1. **Be Clear**: Explicit instructions work best
2. **Be Specific**: Avoid ambiguity
3. **Set Format**: Specify output format if needed
4. **Add Constraints**: Include any limitations

## 🎯 Few-shot Prompting

### When to Use

✅ **Use few-shot when:**
- Need specific format or style
- Pattern recognition required
- Consistency is important
- Model needs guidance

### Basic Pattern

```python
"""
Example 1:
{input_1} → {output_1}

Example 2:
{input_2} → {output_2}

Example 3:
{input_3} → {output_3}

Now solve:
{new_input}
"""
```

### Examples

#### Format Consistency

```python
"""
Format examples:

Input: "John Doe, 30, Engineer"
Output: {
  "name": "John Doe",
  "age": 30,
  "profession": "Engineer"
}

Input: "Jane Smith, 25, Designer"
Output: {
  "name": "Jane Smith",
  "age": 25,
  "profession": "Designer"
}

Now format: "Bob Johnson, 35, Developer"
"""
```

#### Style Matching

```python
"""
Write in this style:

Example 1:
Topic: "Machine Learning"
Output: "Machine learning is a subset of artificial intelligence..."

Example 2:
Topic: "Cloud Computing"
Output: "Cloud computing refers to the delivery of computing services..."

Now write about: "Data Science"
"""
```

#### Pattern Recognition

```python
"""
Identify the pattern:

Example 1: 2, 4, 6, 8 → Even numbers
Example 2: 1, 3, 5, 7 → Odd numbers
Example 3: 10, 20, 30, 40 → Multiples of 10

Identify: 3, 6, 9, 12
"""
```

## 💡 Advanced Few-shot Techniques

### 1. Diverse Examples

```python
"""
Show variety in examples:

Example 1: Simple case
{simple_example}

Example 2: Complex case
{complex_example}

Example 3: Edge case
{edge_case_example}
"""
```

### 2. Progressive Complexity

```python
"""
Examples from simple to complex:

Example 1: Basic
{basic_example}

Example 2: Intermediate
{intermediate_example}

Example 3: Advanced
{advanced_example}
"""
```

### 3. Error Examples

```python
"""
Show correct and incorrect:

Correct Example:
{correct}

Incorrect Example:
{incorrect}
Why it's wrong: {explanation}

Now solve: {new_task}
"""
```

## 📊 Zero-shot vs Few-shot

| Aspect | Zero-shot | Few-shot |
|--------|-----------|----------|
| Examples | 0 | 2-5 |
| Speed | Faster | Slightly slower |
| Consistency | Variable | Higher |
| Format Control | Limited | Better |
| Use Case | Simple tasks | Pattern learning |

## 🎯 Best Practices

### Zero-shot

1. **Be explicit**: Clear instructions
2. **Specify format**: If format matters
3. **Add constraints**: Set boundaries
4. **Use keywords**: Important terms help

### Few-shot

1. **Choose good examples**: Representative samples
2. **Show variety**: Different cases
3. **Be consistent**: Same format across examples
4. **Limit examples**: 2-5 is usually optimal
5. **Order matters**: Put best examples first

## 🔧 Combining Techniques

### Zero-shot + Role

```python
"""
You are a Python expert.
Write a function to calculate factorial.
"""
```

### Few-shot + Chain of Thought

```python
"""
Example 1:
Problem: 2 + 3
Step 1: Add 2 and 3
Step 2: Result is 5
Answer: 5

Example 2:
Problem: 5 * 4
Step 1: Multiply 5 and 4
Step 2: Result is 20
Answer: 20

Now solve: 10 / 2
"""
```

## 📋 Example Prompts

### Zero-shot Example

```python
"""
Analyze this code for security vulnerabilities.
Provide:
1. List of issues
2. Severity level
3. Recommendations
"""
```

### Few-shot Example

```python
"""
Extract dates in this format:

Text: "Meeting on 2024-01-15"
Date: 2024-01-15

Text: "Event scheduled for March 20, 2024"
Date: 2024-03-20

Text: "Deadline: 12/31/2024"
Date: 2024-12-31

Now extract from: "Conference on January 5th, 2024"
"""
```

## 🔗 Additional Resources

- [Few-shot Learning Guide](https://www.promptingguide.ai/techniques/fewshot)
- [In-context Learning](https://www.promptingguide.ai/techniques/fewshot)

---

**Related**: [Chain of Thought](./chain-of-thought/README.md) | [Role-based Prompting](./role-based/README.md)

