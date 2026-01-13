# Role-Based Prompting

## 🎯 Overview

Role-based prompting assigns a specific persona, expertise, or role to the AI model, guiding it to respond from that perspective.

## 📖 What is Role-Based Prompting?

Role-based prompting involves explicitly defining who the AI is (its role, expertise, background) before giving it a task. This helps the model adopt appropriate knowledge, tone, and approach.

### Basic Example

```python
# Without role
"Explain machine learning"

# With role
"You are a senior data scientist with 15 years of experience.
Explain machine learning to a beginner audience."
```

## 🎯 When to Use Role-Based Prompting

### Best For:
- ✅ Domain-specific expertise needed
- ✅ Professional tone required
- ✅ Specialized terminology
- ✅ Expert perspective
- ✅ Teaching or explaining

### Not Ideal For:
- ❌ Simple factual questions
- ❌ Generic tasks
- ❌ No specific expertise needed

## 👥 Common Roles

### Technical Roles

```python
"""
You are a senior software architect specializing in:
- Microservices architecture
- Cloud-native applications
- System scalability

Design a system for...
"""
```

### Professional Roles

```python
"""
You are a business consultant with expertise in:
- Strategic planning
- Market analysis
- Organizational development

Analyze this business case...
"""
```

### Educational Roles

```python
"""
You are a university professor teaching computer science.
Your students are beginners with basic programming knowledge.

Explain recursion in a way that's easy to understand...
"""
```

## 💡 Role Definition Patterns

### Pattern 1: Simple Role

```python
"You are a {role}. {task}"
```

### Pattern 2: Detailed Role

```python
"""
You are a {role} with:
- {years} years of experience
- Expertise in: {expertise areas}
- Specialization in: {specializations}

{task}
"""
```

### Pattern 3: Role + Context

```python
"""
Role: {role}
Context: {situation}
Task: {task}
Output Format: {format}
"""
```

## 🎨 Role Examples

### Software Engineer

```python
"""
You are a senior software engineer at a tech company.
You specialize in Python, system design, and code quality.

Review this code and provide:
1. Code quality assessment
2. Performance analysis
3. Security review
4. Improvement suggestions
"""
```

### Data Scientist

```python
"""
You are a data scientist with expertise in:
- Machine learning
- Statistical analysis
- Data visualization
- Python and R

Analyze this dataset and provide insights...
"""
```

### Technical Writer

```python
"""
You are a technical writer specializing in:
- Software documentation
- API documentation
- User guides
- Clear, concise writing

Write documentation for this API...
"""
```

### Business Analyst

```python
"""
You are a business analyst with experience in:
- Requirements analysis
- Process improvement
- Stakeholder communication
- Data-driven decision making

Analyze this business process...
"""
```

## 🔧 Advanced Techniques

### 1. Multiple Roles

```python
"""
You are a team of experts:
- Senior Developer: Code quality and architecture
- Security Expert: Security and compliance
- DevOps Engineer: Deployment and infrastructure

Collaboratively review this system...
"""
```

### 2. Role Evolution

```python
"""
You are a junior developer learning from a senior mentor.

First, attempt to solve this problem yourself.
Then, the senior mentor will review your solution
and provide feedback.
"""
```

### 3. Role Constraints

```python
"""
You are a security auditor.
Your role requires:
- Strict adherence to security best practices
- Zero tolerance for vulnerabilities
- Detailed documentation of findings

Audit this code for security issues...
"""
```

## 📊 Role Selection Guide

| Role | Best For | Tone | Expertise Level |
|------|----------|------|-----------------|
| Senior Engineer | Code review, architecture | Professional | High |
| Teacher | Explanations, tutorials | Friendly | Medium |
| Consultant | Analysis, strategy | Formal | High |
| Developer | Implementation | Technical | Medium |
| Analyst | Data analysis | Objective | Medium |

## 💡 Best Practices

### 1. Be Specific

```python
# ✅ Good: Specific role
"You are a Python backend developer with 10 years of experience
specializing in Django and REST APIs"

# ❌ Avoid: Vague role
"You are a developer"
```

### 2. Include Relevant Expertise

```python
"""
You are a {role} with expertise in:
- {relevant skill 1}
- {relevant skill 2}
- {relevant skill 3}
"""
```

### 3. Set Expectations

```python
"""
You are a {role}.
Your responses should:
- Be {tone}
- Focus on {focus areas}
- Avoid {what to avoid}
"""
```

### 4. Combine with Other Techniques

```python
"""
You are a {role}.

Task: {task}

Think step by step:
1. {step 1}
2. {step 2}
3. {step 3}
"""
```

## 🎯 Use Cases

### Code Review

```python
"""
You are a senior code reviewer.
Review this code for:
- Code quality
- Best practices
- Performance
- Security
"""
```

### Documentation

```python
"""
You are a technical writer.
Write clear, concise documentation that:
- Explains concepts simply
- Includes examples
- Follows documentation standards
"""
```

### Problem Solving

```python
"""
You are a systems architect.
Design a solution that:
- Meets all requirements
- Is scalable and maintainable
- Follows industry best practices
"""
```

## 🔗 Additional Resources

- [Role-Based Prompting Guide](https://www.promptingguide.ai/techniques/role)
- [Persona Development](https://www.promptingguide.ai/techniques/persona)

---

**Related**: [Chain of Thought](./chain-of-thought/README.md) | [Structured Output](./structured-output/README.md)

