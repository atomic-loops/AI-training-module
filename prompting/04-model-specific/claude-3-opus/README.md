# Claude 3 Opus Prompting Guide

## 🎯 Overview

Claude 3 Opus is Anthropic's most capable model, designed for complex reasoning, analysis, and high-quality outputs. It excels at nuanced understanding and sophisticated tasks.

## 📊 Model Specifications

- **Context Window**: 200K tokens
- **Output Limit**: 4K tokens (can be extended)
- **Best For**: Complex reasoning, analysis, high-quality outputs
- **Cost**: Highest among Claude models
- **Speed**: Slower but highest quality

## 🎯 Optimal Prompting Styles

### 1. Complex Reasoning

Claude 3 Opus excels at sophisticated reasoning:

```python
"""
You are an expert analyst. Analyze this complex situation:

{situation}

Consider:
- Multiple perspectives and viewpoints
- Underlying assumptions
- Potential implications
- Alternative interpretations
- Long-term consequences

Provide a nuanced, comprehensive analysis.
"""
```

### 2. Conversational and Thoughtful

Claude responds well to conversational prompts:

```python
"""
Let's think through this together:

{problem}

I'd appreciate your thoughts on:
- The core issues
- Different approaches we could take
- Pros and cons of each
- Your recommendation and why

Feel free to explore the nuances.
"""
```

### 3. Detailed Analysis

```python
"""
Perform a deep analysis of:

{topic}

Structure your analysis:
1. Context and background
2. Key factors and variables
3. Multiple perspectives
4. Potential scenarios
5. Risks and opportunities
6. Recommendations with rationale
"""
```

## 💡 Best Practices

### 1. Encourage Deep Thinking

```python
"""
Think deeply about this problem:

{problem}

Consider:
- What are we really trying to solve?
- What assumptions are we making?
- What are the edge cases?
- What could go wrong?
- What are alternative approaches?
"""
```

### 2. Request Nuanced Responses

```python
"""
Provide a nuanced analysis that considers:

- The complexity of the issue
- Multiple valid perspectives
- Trade-offs and compromises
- Context-dependent factors
- Unintended consequences
"""
```

### 3. Use the Large Context Window

```python
"""
You have access to this extensive document (100K+ tokens):
{document}

Provide a comprehensive analysis that:
- Synthesizes information across sections
- Identifies themes and patterns
- Connects related concepts
- Provides deep insights
"""
```

### 4. Ask for Explanations

```python
"""
Explain your reasoning:

{task}

For each major decision or conclusion:
- Explain why you chose this approach
- What alternatives you considered
- What evidence supports your view
- What limitations exist
"""
```

## 🎨 Use Cases

### Best For:
- ✅ **Complex analysis**: Deep, nuanced analysis
- ✅ **Strategic thinking**: Long-term planning
- ✅ **Research synthesis**: Combining multiple sources
- ✅ **Philosophical questions**: Abstract reasoning
- ✅ **Creative problem-solving**: Novel approaches
- ✅ **Ethical considerations**: Moral reasoning
- ✅ **Academic writing**: Scholarly analysis

### Not Ideal For:
- ❌ **Simple tasks**: Overkill, use Claude 3.5 Sonnet
- ❌ **Quick responses**: Slower than other models
- ❌ **Cost-sensitive**: Most expensive Claude model
- ❌ **High-speed requirements**: Not optimized for speed

## 📋 Example Prompts

### Strategic Analysis

```python
"""
Analyze this strategic decision:

{decision_context}

Consider:
1. Short-term and long-term implications
2. Stakeholder perspectives
3. Risk assessment
4. Opportunity costs
5. Alternative strategies
6. Implementation challenges
7. Success metrics

Provide a comprehensive strategic analysis.
"""
```

### Research Synthesis

```python
"""
Synthesize insights from these research papers:

{research_papers}

Provide:
1. Common themes across papers
2. Conflicting findings and why
3. Gaps in current research
4. Emerging patterns
5. Practical implications
6. Future research directions
"""
```

### Ethical Analysis

```python
"""
Analyze the ethical dimensions of:

{ethical_issue}

Consider:
1. Different ethical frameworks
2. Conflicting values
3. Stakeholder impacts
4. Long-term consequences
5. Precedents and analogies
6. Balanced perspective

Provide a thoughtful ethical analysis.
"""
```

## 🔧 Advanced Techniques

### 1. Multi-Perspective Analysis

```python
"""
Analyze from multiple perspectives:

{issue}

Perspective 1: {viewpoint_1}
Perspective 2: {viewpoint_2}
Perspective 3: {viewpoint_3}

For each:
- Key arguments
- Strengths and weaknesses
- When it applies
- Limitations

Then synthesize into balanced view.
"""
```

### 2. Socratic Method

```python
"""
Use Socratic questioning to explore:

{topic}

Ask and answer:
1. What do we know for certain?
2. What assumptions are we making?
3. What evidence supports this?
4. What alternative explanations exist?
5. What would we need to know to be sure?
6. What are the implications?
"""
```

### 3. Scenario Planning

```python
"""
Develop scenarios for:

{situation}

For each scenario:
- Conditions that lead to it
- Likelihood
- Key characteristics
- Implications
- Preparation strategies

Scenarios:
1. Best case
2. Most likely
3. Worst case
4. Wild card
"""
```

## 📊 Performance Tips

1. **Encourage depth**: Ask for thorough analysis
2. **Request reasoning**: Claude excels at explaining
3. **Use large context**: Leverage 200K tokens
4. **Be conversational**: Natural language works well
5. **Ask for alternatives**: Claude provides multiple perspectives
6. **Temperature 0-0.3**: For analytical tasks



**Related**: [Claude 3.5 Sonnet Guide](./claude-3-5-sonnet/README.md) | [Model Comparison](../README.md)

