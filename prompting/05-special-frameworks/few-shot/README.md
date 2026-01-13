# Few-shot Prompting

## 🎯 Overview

Few-shot prompting provides a small number of examples (typically 2-5) to the model to demonstrate the desired pattern, format, or behavior. This technique leverages the model's ability to learn from examples in-context.

## 📖 What is Few-shot Prompting?

Few-shot prompting gives the AI model a few examples of the task before asking it to perform the same task on new input. The model learns the pattern from these examples.

### Basic Example

```python
"""
Example 1:
Input: "Hello"
Output: "Bonjour"

Example 2:
Input: "Good morning"
Output: "Bonjour"

Example 3:
Input: "Thank you"
Output: "Merci"

Now translate: "Good evening"
"""
```

## 🎯 When to Use Few-shot Prompting

### Best For:
- ✅ **Format consistency**: Need specific output format
- ✅ **Pattern learning**: Model needs to learn a pattern
- ✅ **Style matching**: Match a specific writing style
- ✅ **Complex tasks**: Tasks that benefit from examples
- ✅ **Consistency**: When consistency across outputs is critical

### Not Ideal For:
- ❌ **Simple tasks**: Overkill for straightforward requests
- ❌ **No clear pattern**: When examples don't help
- ❌ **Very long examples**: Takes up too much context
- ❌ **Inconsistent examples**: Confusing patterns

## 📝 Few-shot Prompting Patterns

### Pattern 1: Input-Output Pairs

```python
"""
Example 1:
Input: {input_1}
Output: {output_1}

Example 2:
Input: {input_2}
Output: {output_2}

Example 3:
Input: {input_3}
Output: {output_3}

Now process:
Input: {new_input}
"""
```

### Pattern 2: Step-by-step Examples

```python
"""
Example 1:
Problem: {problem_1}
Step 1: {step_1}
Step 2: {step_2}
Answer: {answer_1}

Example 2:
Problem: {problem_2}
Step 1: {step_1}
Step 2: {step_2}
Answer: {answer_2}

Now solve:
Problem: {new_problem}
"""
```

### Pattern 3: Format Examples

```python
"""
Format examples:

Example 1:
{formatted_example_1}

Example 2:
{formatted_example_2}

Example 3:
{formatted_example_3}

Now format: {new_data}
"""
```

## 💡 Best Practices

### 1. Choose Representative Examples

```python
# ✅ Good: Diverse examples
"""
Example 1: Simple case
Example 2: Medium complexity
Example 3: Edge case
"""

# ❌ Avoid: All similar examples
"""
Example 1: Very similar to Example 2
Example 2: Very similar to Example 3
"""
```

### 2. Show Variety

```python
"""
Example 1: Positive sentiment
Input: "I love this product!"
Output: {"sentiment": "positive", "score": 0.9}

Example 2: Negative sentiment
Input: "This is terrible."
Output: {"sentiment": "negative", "score": 0.1}

Example 3: Neutral sentiment
Input: "It's okay."
Output: {"sentiment": "neutral", "score": 0.5}
"""
```

### 3. Keep Examples Consistent

```python
# ✅ Good: Same format
"""
Example 1: Input → Output
Example 2: Input → Output
Example 3: Input → Output
"""

# ❌ Avoid: Inconsistent format
"""
Example 1: Input → Output
Example 2: Different format
Example 3: Another format
"""
```

### 4. Optimal Number of Examples

- **2-3 examples**: Good for simple patterns
- **3-5 examples**: Optimal for most tasks
- **5+ examples**: May be overkill, use only if needed

### 5. Order Matters

```python
# ✅ Good: Best examples first
"""
Example 1: Perfect example
Example 2: Good example
Example 3: Another good example
"""

# ❌ Avoid: Weak examples first
"""
Example 1: Weak example
Example 2: Better example
Example 3: Best example
"""
```

## 🎨 Real-World Examples

### Example 1: Data Extraction

```python
"""
Extract information in this format:

Example 1:
Text: "John Doe, age 30, works as an engineer"
Output: {
  "name": "John Doe",
  "age": 30,
  "profession": "engineer"
}

Example 2:
Text: "Jane Smith is 25 years old and a designer"
Output: {
  "name": "Jane Smith",
  "age": 25,
  "profession": "designer"
}

Example 3:
Text: "Bob Johnson, 35, software developer"
Output: {
  "name": "Bob Johnson",
  "age": 35,
  "profession": "software developer"
}

Now extract from: "Alice Brown, 28, data scientist"
"""
```

### Example 2: Code Generation

```python
"""
Generate functions in this style:

Example 1:
Task: "Reverse a string"
Code:
def reverse_string(s: str) -> str:
    \"\"\"Reverse a string.\"\"\"
    return s[::-1]

Example 2:
Task: "Count words"
Code:
def count_words(text: str) -> int:
    \"\"\"Count words in text.\"\"\"
    return len(text.split())

Example 3:
Task: "Check palindrome"
Code:
def is_palindrome(s: str) -> bool:
    \"\"\"Check if string is palindrome.\"\"\"
    return s == s[::-1]

Now generate: "Find maximum in list"
"""
```

### Example 3: Text Classification

```python
"""
Classify text with confidence score:

Example 1:
Text: "This movie is amazing!"
Category: "positive"
Confidence: 0.95

Example 2:
Text: "I hate this product."
Category: "negative"
Confidence: 0.90

Example 3:
Text: "It's okay, nothing special."
Category: "neutral"
Confidence: 0.75

Now classify: "This is the best day ever!"
"""
```

## 🔧 Advanced Techniques

### 1. Progressive Complexity

```python
"""
Examples from simple to complex:

Example 1: Basic
{simple_example}

Example 2: Intermediate
{medium_example}

Example 3: Advanced
{complex_example}

Now solve: {new_task}
"""
```

### 2. Error Examples

```python
"""
Show correct and incorrect:

Correct Example 1:
{correct_1}

Incorrect Example:
{incorrect}
Why wrong: {explanation}

Correct Example 2:
{correct_2}

Now solve: {new_task}
"""
```

### 3. Multiple Patterns

```python
"""
Pattern A examples:
Example 1: {pattern_a_1}
Example 2: {pattern_a_2}

Pattern B examples:
Example 1: {pattern_b_1}
Example 2: {pattern_b_2}

Identify which pattern applies and solve: {new_task}
"""
```

### 4. Few-shot with Chain of Thought

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

Now solve step by step: 10 / 2
"""
```

## 📊 Few-shot vs Zero-shot

| Aspect | Zero-shot | Few-shot |
|--------|-----------|----------|
| Examples | 0 | 2-5 |
| Consistency | Variable | Higher |
| Format Control | Limited | Better |
| Context Usage | Less | More |
| Best For | Simple tasks | Pattern learning |

## 🎯 Use Cases

### Code Formatting

```python
"""
Format code comments like this:

Example 1:
def calculate_sum(a, b):
    # Calculate sum of two numbers
    return a + b

Example 2:
def find_max(numbers):
    # Find maximum value in list
    return max(numbers)

Now format: {new_function}
"""
```

### API Response Format

```python
"""
Format API responses like this:

Example 1:
{
  "status": "success",
  "data": {...},
  "timestamp": "2024-01-15T10:30:00Z"
}

Example 2:
{
  "status": "error",
  "error": {...},
  "timestamp": "2024-01-15T10:31:00Z"
}

Now format: {new_response}
"""
```

### Email Generation

```python
"""
Write emails in this style:

Example 1:
Subject: Meeting Request
Body: Hi {name}, I'd like to schedule a meeting...

Example 2:
Subject: Project Update
Body: Dear {name}, I'm writing to update you...

Now write: {new_email_request}
"""
```

## 💡 Tips for Effective Few-shot Prompting

1. **Quality over quantity**: 3 good examples > 5 mediocre ones
2. **Show diversity**: Cover different cases and edge cases
3. **Be consistent**: Same format across all examples
4. **Test examples**: Make sure examples work correctly
5. **Update as needed**: Refine examples based on results

## 🔗 Additional Resources

- [Few-shot Learning Research](https://www.promptingguide.ai/techniques/fewshot)
- [In-context Learning](https://www.promptingguide.ai/techniques/fewshot)
- [Example Selection Strategies](https://www.promptingguide.ai/)

## 📋 Few-shot Checklist

When creating few-shot prompts:

- [ ] Examples are representative of the task
- [ ] Examples show variety (different cases)
- [ ] Examples follow consistent format
- [ ] Optimal number of examples (2-5)
- [ ] Best examples are shown first
- [ ] Examples are clear and correct
- [ ] Examples match desired output style

---

**Related**: [Zero-shot Prompting](./zero-shot/README.md) | [Chain of Thought](./chain-of-thought/README.md) | [Structured Output](./structured-output/README.md)

