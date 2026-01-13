# Structured Output Generation

## 🎯 Overview

Structured output prompting ensures AI models generate data in specific, machine-readable formats like JSON, XML, or custom schemas.

## 📖 What is Structured Output?

Structured output is data formatted according to a predefined schema, making it easy to parse, validate, and integrate into applications.

### Why Use Structured Output?

- ✅ **Consistency**: Predictable format every time
- ✅ **Integration**: Easy to use in APIs and applications
- ✅ **Validation**: Can be automatically validated
- ✅ **Parsing**: Simple to extract specific fields

## 🎯 JSON Output

### Basic JSON Prompt

```python
"""
Generate output as JSON:

{
  "name": "...",
  "age": ...,
  "email": "..."
}
"""
```

### Complex JSON Schema

```python
"""
Return a JSON object with this structure:

{
  "summary": {
    "total": number,
    "average": number,
    "max": number,
    "min": number
  },
  "data": [
    {
      "id": number,
      "value": number,
      "category": "string"
    }
  ],
  "metadata": {
    "timestamp": "ISO 8601 date",
    "source": "string"
  }
}
"""
```

## 📋 XML Output

### XML Format

```python
"""
Generate output as XML:

<response>
  <status>success</status>
  <data>
    <item>
      <id>1</id>
      <name>Item Name</name>
    </item>
  </data>
</response>
"""
```

## 📊 CSV Output

### CSV Format

```python
"""
Generate output as CSV with headers:

Name,Age,Email,Status
John Doe,30,john@example.com,Active
Jane Smith,25,jane@example.com,Active
"""
```

## 🎨 Custom Formats

### Markdown Tables

```python
"""
Format output as a markdown table:

| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Value 1  | Value 2  | Value 3  |
"""
```

### YAML Format

```python
"""
Generate output as YAML:

name: "John Doe"
age: 30
email: "john@example.com"
status: "active"
"""
```

## 🔧 Advanced Techniques

### 1. Schema Validation

```python
"""
Generate JSON that validates against this schema:

{
  "type": "object",
  "properties": {
    "name": {"type": "string", "minLength": 1},
    "age": {"type": "integer", "minimum": 0},
    "email": {"type": "string", "format": "email"}
  },
  "required": ["name", "age", "email"]
}
"""
```

### 2. Conditional Fields

```python
"""
Generate JSON with conditional structure:

{
  "type": "user",
  "id": number,
  "name": "string",
  "email": "string",
  "role": "admin" | "user",
  "permissions": ["string"] (only if role is "admin")
}
"""
```

### 3. Nested Structures

```python
"""
Generate nested JSON:

{
  "user": {
    "profile": {
      "name": "string",
      "age": number
    },
    "settings": {
      "theme": "string",
      "notifications": boolean
    }
  }
}
"""
```

## 💡 Best Practices

### 1. Be Explicit About Format

```python
# ✅ Good: Explicit format
"Return ONLY valid JSON, no additional text"

# ❌ Avoid: Ambiguous
"Return JSON"
```

### 2. Provide Examples

```python
"""
Format like this example:

{
  "result": "success",
  "data": {...}
}

Now generate for: {task}
"""
```

### 3. Specify Constraints

```python
"""
Generate JSON with:
- All strings must be non-empty
- All numbers must be positive
- All dates in ISO 8601 format
- No null values
"""
```

### 4. Error Handling

```python
"""
If data is unavailable, return:

{
  "status": "error",
  "message": "string",
  "code": number
}

Otherwise return:

{
  "status": "success",
  "data": {...}
}
"""
```

## 🎯 Use Cases

### API Response Generation

```python
"""
Generate API response:

{
  "status": "success" | "error",
  "code": 200 | 400 | 500,
  "data": {...} (if status is success),
  "error": {...} (if status is error)
}
"""
```

### Data Extraction

```python
"""
Extract information from this text as JSON:

{text}

Extract:
- Names (array of strings)
- Dates (array of ISO dates)
- Amounts (array of numbers)
- Summary (string)
"""
```

### Configuration Generation

```python
"""
Generate configuration file as JSON:

{
  "app": {
    "name": "string",
    "version": "string",
    "environment": "production" | "development"
  },
  "database": {
    "host": "string",
    "port": number,
    "name": "string"
  }
}
"""
```

## 🔗 Model-Specific Features

### OpenAI Function Calling

```python
# Use function calling for structured output
functions = [{
    "name": "extract_data",
    "parameters": {
        "type": "object",
        "properties": {
            "name": {"type": "string"},
            "age": {"type": "integer"}
        }
    }
}]
```

### Anthropic Structured Outputs

```python
# Claude 3.5+ supports native structured outputs
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    messages=[...],
    response_format={"type": "json_schema", "schema": {...}}
)
```

## 📋 Example Prompts

### Example 1: Data Extraction

```python
"""
Extract product information from this text as JSON:

{product_text}

Format:
{
  "name": "string",
  "price": number,
  "description": "string",
  "features": ["string"],
  "availability": boolean
}
"""
```

### Example 2: Analysis Results

```python
"""
Analyze this code and return JSON:

{code}

{
  "complexity": "low" | "medium" | "high",
  "issues": [
    {
      "type": "bug" | "security" | "performance",
      "severity": "low" | "medium" | "high",
      "description": "string",
      "line": number
    }
  ],
  "recommendations": ["string"]
}
"""
```

## 🔗 Additional Resources

- [JSON Schema](https://json-schema.org/)
- [OpenAI Function Calling](https://platform.openai.com/docs/guides/function-calling)
- [Anthropic Structured Outputs](https://docs.anthropic.com/claude/docs/structured-outputs)

---

**Related**: [Chain of Thought](./chain-of-thought/README.md) | [Role-based Prompting](./role-based/README.md)

