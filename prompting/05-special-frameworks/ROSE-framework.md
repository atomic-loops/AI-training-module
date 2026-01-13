# ROSE Framework: Rules Observation

## 🎯 Overview

ROSE (Rules Observation) is a prompting framework designed to ensure AI models strictly adhere to specific rules, guidelines, or constraints. It's particularly useful for compliance, legal, policy, and regulatory scenarios.

## 📖 What is ROSE?

ROSE stands for **Rules Observation** - a framework that explicitly defines rules and requires the model to observe and follow them strictly.

### Core Principle

The ROSE framework ensures that:
- **Rules are explicit**: Clearly stated and unambiguous
- **Compliance is mandatory**: Rules must be followed
- **Violations are detected**: Model identifies rule violations
- **Corrections are made**: Model corrects violations

## 🎯 When to Use ROSE

### Best For:
- ✅ Legal document generation
- ✅ Policy compliance
- ✅ Regulatory requirements
- ✅ Security protocols
- ✅ Quality standards
- ✅ Format specifications
- ✅ Business rules

### Not Ideal For:
- ❌ Creative writing
- ❌ Exploratory tasks
- ❌ Flexible requirements
- ❌ Subjective tasks

## 📋 ROSE Framework Structure

### Basic Pattern

```python
"""
ROSE Framework Application:

RULES:
1. {rule_1}
2. {rule_2}
3. {rule_3}

OBSERVATION:
- Check each rule
- Identify violations
- Document compliance

ENFORCEMENT:
- Correct violations
- Verify compliance
- Confirm adherence

Task: {task}
"""
```

## 💡 ROSE Implementation Patterns

### Pattern 1: Explicit Rules

```python
"""
ROSE Framework:

RULES TO OBSERVE:
1. All code must include error handling
2. All functions must have type hints
3. All functions must have docstrings
4. Maximum function length: 50 lines
5. No hardcoded values

Task: Write a Python function to process user data

OBSERVATION CHECKLIST:
- [ ] Error handling included
- [ ] Type hints present
- [ ] Docstring added
- [ ] Function length < 50 lines
- [ ] No hardcoded values

Generate code that follows ALL rules.
"""
```

### Pattern 2: Rule Validation

```python
"""
ROSE Framework:

RULES:
1. Email must be valid format
2. Age must be 18-100
3. Name must be non-empty
4. Phone must be 10 digits

Task: Validate user input

PROCESS:
1. Check each rule
2. Report violations
3. Provide corrections
4. Confirm compliance

Input: {user_input}
"""
```

### Pattern 3: Compliance Checking

```python
"""
ROSE Framework:

COMPLIANCE RULES:
1. GDPR: No personal data without consent
2. Security: All data encrypted
3. Privacy: User data anonymized
4. Access: Role-based permissions

Task: Review this code for compliance

For each rule:
- Check compliance
- Identify violations
- Suggest fixes
- Verify adherence
"""
```

## 🎨 Real-World Examples

### Example 1: Code Review with Rules

```python
"""
ROSE Framework - Code Review:

CODING RULES:
1. PEP 8 style guide compliance
2. All functions < 100 lines
3. Test coverage > 80%
4. No security vulnerabilities
5. Proper error handling

Code to review:
{code}

ROSE PROCESS:
Step 1: Check each rule
Step 2: Document violations
Step 3: Provide compliant version
Step 4: Verify all rules met
"""
```

### Example 2: Legal Document Generation

```python
"""
ROSE Framework - Legal Document:

LEGAL RULES:
1. Must include disclaimer
2. Must specify jurisdiction
3. Must include date
4. Must have signature line
5. Must comply with local laws

Task: Generate privacy policy

ROSE CHECKLIST:
- [ ] Disclaimer included
- [ ] Jurisdiction specified
- [ ] Date present
- [ ] Signature line added
- [ ] Legal compliance verified

Generate document following ALL rules.
"""
```

### Example 3: Data Processing Rules

```python
"""
ROSE Framework - Data Processing:

PROCESSING RULES:
1. No PII in logs
2. Data encrypted at rest
3. Access logged
4. Retention: 90 days max
5. Deletion: Secure wipe

Task: Design data processing pipeline

ROSE VALIDATION:
For each rule:
- Verify implementation
- Check compliance
- Document adherence
"""
```

## 🔧 Advanced ROSE Techniques

### 1. Hierarchical Rules

```python
"""
ROSE Framework:

PRIMARY RULES (Must follow):
1. {critical_rule_1}
2. {critical_rule_2}

SECONDARY RULES (Should follow):
1. {important_rule_1}
2. {important_rule_2}

TERTIARY RULES (Nice to have):
1. {optional_rule_1}
2. {optional_rule_2}

Task: {task}

Prioritize primary rules, then secondary, then tertiary.
"""
```

### 2. Conditional Rules

```python
"""
ROSE Framework:

RULES:
1. If user is admin: Full access
2. If user is regular: Limited access
3. If data is sensitive: Extra encryption
4. If operation is write: Require approval

Task: {task}

Apply rules based on conditions.
"""
```

### 3. Rule Verification Loop

```python
"""
ROSE Framework:

RULES: {rules}

PROCESS:
1. Generate output
2. Check against each rule
3. If violation found:
   - Identify violation
   - Correct output
   - Re-check rules
4. Repeat until all rules satisfied

Task: {task}
"""
```

## 📊 ROSE vs Standard Prompting

| Aspect | Standard | ROSE |
|--------|----------|------|
| Rule Compliance | Implicit | Explicit |
| Violation Detection | Manual | Automatic |
| Correction | Manual | Guided |
| Use Case | General | Compliance |
| Strictness | Flexible | Strict |

## 💡 Best Practices

### 1. Be Explicit

```python
# ✅ Good: Clear rules
"RULE 1: All functions must have docstrings
RULE 2: All functions must have type hints"

# ❌ Avoid: Vague rules
"Follow best practices"
```

### 2. Number Your Rules

```python
# ✅ Good: Numbered
"1. Rule one
2. Rule two
3. Rule three"

# ✅ Also good: Lettered
"A. Rule one
B. Rule two
C. Rule three"
```

### 3. Provide Examples

```python
"""
RULE: All dates in ISO 8601 format

Correct: 2024-01-15
Incorrect: 01/15/2024
Incorrect: January 15, 2024
"""
```

### 4. Check Compliance

```python
"""
After generating output:
1. Verify each rule
2. List any violations
3. Provide corrected version
"""
```

## 🎯 Use Cases

### Compliance

```python
"""
ROSE Framework - Compliance:

REGULATORY RULES:
1. GDPR Article 6: Legal basis required
2. GDPR Article 13: Information provided
3. GDPR Article 17: Right to deletion

Verify compliance with each article.
"""
```

### Security

```python
"""
ROSE Framework - Security:

SECURITY RULES:
1. No SQL injection vulnerabilities
2. Input validation required
3. Authentication mandatory
4. Encryption for sensitive data

Review code for security rule compliance.
"""
```

### Quality Standards

```python
"""
ROSE Framework - Quality:

QUALITY RULES:
1. Code coverage > 80%
2. All tests passing
3. No critical bugs
4. Documentation complete

Verify quality standards met.
"""
```

## 🔗 Additional Resources

- [Compliance Frameworks](https://www.promptingguide.ai/)
- [Rule-Based Systems](https://www.promptingguide.ai/)

## 📋 ROSE Checklist

When using ROSE framework:

- [ ] Rules are explicitly stated
- [ ] Rules are numbered or clearly organized
- [ ] Compliance checking is built into prompt
- [ ] Violation detection is specified
- [ ] Correction process is defined
- [ ] Verification step is included

---

**Related**: [Structured Output](./structured-output/README.md) | [Chain of Thought](./chain-of-thought/README.md)

