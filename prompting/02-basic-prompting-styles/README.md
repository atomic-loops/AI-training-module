# Module 2: Basic Prompting Styles

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Use direct prompting effectively
- Apply instructional prompting techniques
- Craft question-based prompts
- Utilize contextual prompting
- Create template-based prompts
- Choose the right style for different scenarios

## 📝 Direct Prompting

### What is Direct Prompting?

Direct prompting is straightforward, explicit instructions without additional context or structure.

### Characteristics

- **Simple and clear**: Direct instructions
- **No ambiguity**: Explicit requirements
- **Quick to write**: Minimal setup needed
- **Best for**: Simple, well-defined tasks

### Examples

```python
# Basic direct prompt
"Write a Python function to reverse a string"

# With constraints
"Write a Python function to reverse a string. 
Use only built-in functions, no external libraries."

# With output format
"Write a Python function to reverse a string.
Return the function code with a docstring."
```

### When to Use

✅ **Use direct prompting when:**
- Task is simple and well-defined
- No special context needed
- Quick, one-off requests
- Model is familiar with the domain

❌ **Avoid when:**
- Complex, multi-step tasks
- Need specific style or tone
- Require extensive context
- Need structured output

## 📋 Instructional Prompting

### What is Instructional Prompting?

Instructional prompting provides step-by-step guidance, breaking complex tasks into manageable steps.

### Characteristics

- **Structured**: Clear steps or phases
- **Sequential**: Logical flow of instructions
- **Detailed**: Specific guidance at each step
- **Best for**: Complex, multi-step tasks

### Examples

```python
# Step-by-step instructions
"""
Task: Analyze a dataset
Steps:
1. Load the dataset and examine its structure
2. Check for missing values and data quality issues
3. Calculate summary statistics for numeric columns
4. Identify correlations between variables
5. Create visualizations for key insights
6. Provide recommendations based on findings
"""

# Phase-based instructions
"""
Phase 1: Understanding
- Read the problem statement
- Identify key requirements
- List assumptions

Phase 2: Design
- Create a high-level architecture
- Define data structures
- Plan the algorithm

Phase 3: Implementation
- Write the code
- Add error handling
- Include documentation
"""
```

### When to Use

✅ **Use instructional prompting when:**
- Multi-step processes
- Need systematic approach
- Complex problem-solving
- Teaching or explaining concepts

❌ **Avoid when:**
- Simple, single-step tasks
- Quick lookups or definitions
- Tasks that don't need structure

## ❓ Question-Based Prompting

### What is Question-Based Prompting?

Question-based prompting uses questions to guide the AI's thinking process and exploration.

### Characteristics

- **Exploratory**: Encourages deep thinking
- **Interactive**: Feels like a conversation
- **Comprehensive**: Covers multiple angles
- **Best for**: Analysis, exploration, brainstorming

### Examples

```python
# Single question
"What are the main challenges in implementing microservices architecture?"

# Multiple related questions
"""
What are the advantages of microservices?
What are the main challenges?
How do you handle service communication?
What strategies help with deployment?
"""

# Socratic questioning
"""
What is the problem we're trying to solve?
Why is this problem important?
What are the current solutions?
What are their limitations?
What would an ideal solution look like?
"""
```

### When to Use

✅ **Use question-based prompting when:**
- Exploring a topic
- Need multiple perspectives
- Brainstorming solutions
- Analyzing problems

❌ **Avoid when:**
- Need specific output format
- Want direct answers
- Time-sensitive tasks
- Code generation

## 🎯 Contextual Prompting

### What is Contextual Prompting?

Contextual prompting provides background information, domain knowledge, and relevant details to help the AI understand the situation.

### Characteristics

- **Rich context**: Background information included
- **Domain-specific**: Uses relevant terminology
- **Situational**: Considers the use case
- **Best for**: Domain-specific tasks, complex scenarios

### Examples

```python
# With domain context
"""
Context: You're building a REST API for an e-commerce platform
Task: Design the endpoint structure for product management

Requirements:
- Products have: id, name, price, category, stock
- Need CRUD operations
- Must handle authentication
- Should support pagination and filtering
"""

# With project context
"""
Project: Web application for task management
Tech Stack: Python Flask, PostgreSQL, React
Current State: Basic CRUD implemented
Task: Add user authentication and authorization

Requirements:
- JWT-based authentication
- Role-based access control (admin, user)
- Secure password hashing
- Session management
"""
```

### When to Use

✅ **Use contextual prompting when:**
- Domain-specific knowledge needed
- Building on existing systems
- Need to match specific requirements
- Complex, real-world scenarios

❌ **Avoid when:**
- Generic, universal tasks
- Simple, standalone requests
- No specific context available

## 📄 Template-Based Prompting

### What is Template-Based Prompting?

Template-based prompting uses structured formats with placeholders and sections for consistent, repeatable prompts.

### Characteristics

- **Structured**: Fixed format with sections
- **Reusable**: Template can be used multiple times
- **Consistent**: Same structure across prompts
- **Best for**: Repeated tasks, team collaboration

### Examples

```python
# Code review template
"""
Role: Senior Software Engineer
Task: Code Review
Code:
{code_snippet}

Review Criteria:
- Code quality and readability
- Performance considerations
- Security issues
- Best practices adherence

Output Format:
1. Overall assessment
2. Specific issues (with line numbers)
3. Recommendations
4. Priority fixes
"""

# Analysis template
"""
Role: {role}
Task: {task}
Context: {context}
Data: {data}
Constraints: {constraints}
Output Format: {format}
"""
```

### When to Use

✅ **Use template-based prompting when:**
- Repeating similar tasks
- Team needs consistency
- Standardizing processes
- Building prompt libraries

❌ **Avoid when:**
- One-off, unique requests
- Need flexibility
- Experimental prompts

## 🎨 Combining Styles

### Multi-Style Prompts

You can combine multiple styles for more effective prompts:

```python
"""
[CONTEXTUAL] You're a data scientist working on a customer churn prediction project.
The dataset contains 10,000 customer records with features like age, subscription length, 
and usage patterns.

[INSTRUCTIONAL] Perform the following analysis:
1. Load and explore the dataset
2. Handle missing values and outliers
3. Perform feature engineering
4. Train a classification model
5. Evaluate model performance

[QUESTION-BASED] Consider:
- What features are most predictive?
- What's the optimal model complexity?
- How can we improve accuracy?

[DIRECT] Output the complete Python code with explanations.
"""
```

## 📊 Style Comparison

| Style | Best For | Complexity | Flexibility |
|-------|----------|------------|-------------|
| Direct | Simple tasks | Low | High |
| Instructional | Multi-step tasks | Medium | Medium |
| Question-based | Exploration | Medium | High |
| Contextual | Domain-specific | High | Medium |
| Template | Repeated tasks | Low | Low |

## 📋 Module 2 Exercises

### Exercise 1: Style Application
1. Take the same task
2. Write prompts using each style
3. Compare results and effectiveness
4. Identify which style works best

### Exercise 2: Style Selection
1. Create 5 different scenarios
2. Choose the best prompting style for each
3. Write the prompt
4. Justify your choice

### Exercise 3: Style Combination
1. Create a complex task
2. Combine 2-3 prompting styles
3. Test the combined prompt
4. Refine based on results

## 🔗 Additional Resources

- [Prompt Engineering Patterns](https://www.promptingguide.ai/techniques)
- [Effective Prompt Design](https://platform.openai.com/docs/guides/prompt-engineering)

## ✅ Module 2 Checklist

Before moving to Module 3, ensure you can:

- [ ] Use direct prompting for simple tasks
- [ ] Apply instructional prompting for complex tasks
- [ ] Craft question-based prompts for exploration
- [ ] Utilize contextual prompting with background info
- [ ] Create reusable template-based prompts
- [ ] Combine multiple styles effectively
- [ ] Choose the right style for different scenarios

---

**Next Module**: [Module 3: Advanced Techniques](../03-advanced-techniques/README.md)

