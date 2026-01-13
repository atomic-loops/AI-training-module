# Module 3: Advanced Prompting Techniques

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Implement multi-step reasoning prompts
- Use iterative refinement techniques
- Chain prompts together effectively
- Apply conditional logic in prompts
- Use meta-prompting strategies
- Optimize prompts for better results

## 🔄 Multi-Step Reasoning

### What is Multi-Step Reasoning?

Breaking complex problems into logical steps that the AI follows sequentially.

### Technique

```python
"""
Solve this problem step by step:

Problem: Calculate the total cost of items in a shopping cart

Step 1: Identify all items and their prices
Step 2: Apply any discounts or coupons
Step 3: Calculate subtotal
Step 4: Apply tax rate
Step 5: Calculate final total

Show your work for each step.
"""
```

### Benefits

- **Clear thinking**: Forces logical progression
- **Error detection**: Easier to spot mistakes
- **Transparency**: See the reasoning process
- **Better results**: More accurate outcomes

## 🔁 Iterative Refinement

### What is Iterative Refinement?

Starting with a basic prompt and improving it through multiple iterations based on results.

### Process

```python
# Iteration 1: Basic prompt
"Write a function to sort a list"

# Iteration 2: Add constraints
"Write a Python function to sort a list. 
Use only built-in functions, no external libraries."

# Iteration 3: Add requirements
"Write a Python function to sort a list in ascending order.
- Use only built-in functions
- Handle edge cases (empty list, single element)
- Include type hints
- Add a docstring"

# Iteration 4: Add examples
"Write a Python function to sort a list in ascending order.
- Use only built-in functions
- Handle edge cases
- Include type hints and docstring
- Example: sort_list([3, 1, 4, 1, 5]) returns [1, 1, 3, 4, 5]"
```

### Best Practices

1. **Start simple**: Begin with basic prompt
2. **Test and evaluate**: Check the output quality
3. **Identify gaps**: What's missing or wrong?
4. **Refine incrementally**: Add one improvement at a time
5. **Document changes**: Track what works

## 🔗 Prompt Chaining

### What is Prompt Chaining?

Using the output of one prompt as input to the next, creating a sequence of related prompts.

### Example Workflow

```python
# Prompt 1: Analysis
"""
Analyze this code and identify:
1. Main purpose
2. Key functions
3. Potential issues
"""

# Prompt 2: Use output from Prompt 1
"""
Based on the analysis above, create:
1. A refactored version
2. Unit tests
3. Documentation
"""

# Prompt 3: Use output from Prompt 2
"""
Review the refactored code and tests.
Provide:
1. Code review comments
2. Suggestions for improvement
3. Performance optimizations
"""
```

### Use Cases

- **Code generation**: Analyze → Generate → Test → Review
- **Content creation**: Research → Outline → Write → Edit
- **Problem solving**: Understand → Design → Implement → Validate

## 🎛️ Conditional Logic in Prompts

### What is Conditional Logic?

Using if-then structures to handle different scenarios within a single prompt.

### Technique

```python
"""
Analyze this code snippet:

{code}

If the code has security vulnerabilities:
  - List all vulnerabilities
  - Explain the risks
  - Provide secure alternatives

If the code has performance issues:
  - Identify bottlenecks
  - Suggest optimizations
  - Provide benchmark comparisons

If the code follows best practices:
  - Highlight good practices
  - Suggest minor improvements
  - Provide positive feedback
"""
```

### Advanced Conditional Logic

```python
"""
Process this request based on the type:

If request_type == "code_review":
  - Check code quality
  - Identify bugs
  - Suggest improvements

Else if request_type == "documentation":
  - Generate docstrings
  - Create user guide
  - Add examples

Else if request_type == "testing":
  - Write unit tests
  - Create test cases
  - Add integration tests

Else:
  - Ask for clarification
"""
```

## 🎭 Meta-Prompting

### What is Meta-Prompting?

Using prompts to generate or improve other prompts.

### Technique

```python
"""
You are an expert prompt engineer. Your task is to improve this prompt:

Original prompt: "{original_prompt}"

Analyze the prompt and:
1. Identify weaknesses
2. Suggest improvements
3. Provide an optimized version
4. Explain why the changes improve it
"""
```

### Self-Improving Prompts

```python
"""
Improve this prompt iteratively:

Current prompt: "{current_prompt}"
Previous output: "{previous_output}"

Based on the output quality, refine the prompt to:
- Be more specific
- Add missing context
- Clarify requirements
- Improve structure

Provide the improved prompt.
"""
```

## 🎯 Advanced Optimization Techniques

### 1. Output Formatting

```python
"""
Generate output in this exact format:

{
  "analysis": {
    "summary": "...",
    "key_points": ["...", "..."],
    "recommendations": ["...", "..."]
  },
  "code": "...",
  "examples": ["...", "..."]
}
"""
```

### 2. Constraint Specification

```python
"""
Constraints:
- Maximum 500 words
- Use only Python standard library
- Must be production-ready
- Include error handling
- Follow PEP 8 style guide
"""
```

### 3. Example-Driven Prompting

```python
"""
Generate similar output to these examples:

Example 1:
Input: "Sort a list"
Output: [complete code with explanation]

Example 2:
Input: "Reverse a string"
Output: [complete code with explanation]

Now generate for:
Input: "Find maximum in list"
"""
```

### 4. Role-Based Optimization

```python
"""
You are a senior software architect with 20 years of experience.
You specialize in:
- System design
- Performance optimization
- Security best practices

Design a microservices architecture for...
"""
```

## 🔍 Prompt Analysis Techniques

### Decomposing Complex Prompts

Break large prompts into smaller, manageable parts:

```python
# Instead of one huge prompt, use:
"""
Part 1: Context
{context}

Part 2: Requirements
{requirements}

Part 3: Constraints
{constraints}

Part 4: Output Format
{format}
"""
```

### Prompt Versioning

Track different versions:

```python
# v1: Basic
"Write a function"

# v2: With constraints
"Write a function with error handling"

# v3: With examples
"Write a function with error handling and examples"

# Document what changed and why
```

## 📋 Module 3 Exercises

### Exercise 1: Multi-Step Reasoning
1. Create a complex problem
2. Break it into 5-7 steps
3. Write a prompt with step-by-step reasoning
4. Test and refine

### Exercise 2: Iterative Refinement
1. Start with a basic prompt
2. Create 3-4 iterations
3. Document improvements at each step
4. Compare final output with initial

### Exercise 3: Prompt Chaining
1. Design a 3-step workflow
2. Create prompts for each step
3. Chain them together
4. Test the complete workflow

## 🔗 Additional Resources

- [Advanced Prompt Engineering](https://www.promptingguide.ai/techniques)
- [Prompt Optimization Strategies](https://platform.openai.com/docs/guides/prompt-engineering)

## ✅ Module 3 Checklist

Before moving to Module 4, ensure you can:

- [ ] Implement multi-step reasoning prompts
- [ ] Use iterative refinement effectively
- [ ] Chain prompts together
- [ ] Apply conditional logic
- [ ] Use meta-prompting techniques
- [ ] Optimize prompts for better results
- [ ] Analyze and decompose complex prompts

---

**Next Module**: [Module 4: Model-Specific Prompting](../04-model-specific/README.md)

