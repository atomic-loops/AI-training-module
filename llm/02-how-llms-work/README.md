# Module 2: How LLMs Work

## 🎯 Learning Objectives

By the end of this module, you will understand:
- Basic architecture of LLMs
- How LLMs are trained
- How LLMs generate text
- Key concepts: tokens, embeddings, attention
- The role of neural networks

## 🏗️ Basic Architecture

### Neural Networks

LLMs are built using **neural networks** - computing systems inspired by the human brain:

```
Input Text → Neural Network → Output Text
```

### Transformer Architecture

Modern LLMs use the **Transformer** architecture (introduced in 2017):

- **Encoder**: Understands input text
- **Decoder**: Generates output text
- **Attention Mechanism**: Focuses on relevant parts

### Simplified View

```
Your Prompt
    ↓
Tokenization (break into pieces)
    ↓
Embeddings (convert to numbers)
    ↓
Neural Network Processing
    ↓
Attention (focus on important parts)
    ↓
Text Generation
    ↓
Response
```

## 📚 Training Process

### Step 1: Data Collection

LLMs are trained on **massive datasets**:
- Books, articles, websites
- Code repositories
- Conversations
- Scientific papers
- And much more!

**Example**: GPT-3 was trained on ~500 billion tokens of text

### Step 2: Pre-training

The model learns to:
- Predict the next word in a sentence
- Understand language patterns
- Learn grammar, facts, and relationships

**Analogy**: Like learning to read by reading millions of books

### Step 3: Fine-tuning (Optional)

Some models are further trained on:
- Specific tasks
- Domain knowledge
- Safety guidelines
- Human preferences

## 🔤 Key Concepts

### Tokens

**Tokens** are pieces of text the model processes:

```
"Hello world" → ["Hello", " world"]
"GPT-4" → ["GPT", "-", "4"]
```

- Words are often split into tokens
- Models process tokens, not words
- Token limits affect input/output length

### Embeddings

**Embeddings** convert text to numbers:

```
"cat" → [0.2, -0.5, 0.8, ...]
"dog" → [0.3, -0.4, 0.7, ...]
```

- Words with similar meanings have similar numbers
- Allows the model to understand relationships
- Enables mathematical operations on text

### Attention Mechanism

**Attention** helps the model focus on relevant parts:

```
Input: "The cat sat on the mat"
When generating "mat", the model pays attention to:
- "cat" (subject)
- "sat" (verb)
- "on" (preposition)
```

- Like highlighting important words
- Helps understand context
- Enables long-range dependencies

## 🎯 How LLMs Generate Text

### Step-by-Step Process

1. **Receive Input**: Your prompt
2. **Tokenize**: Break into tokens
3. **Process**: Neural network analyzes
4. **Predict**: What comes next
5. **Generate**: One token at a time
6. **Repeat**: Until complete

### Example

```
Prompt: "Write a haiku about coding"

Step 1: Process "Write a haiku about coding"
Step 2: Predict first word: "Code"
Step 3: Predict next: " flows"
Step 4: Predict next: " like"
Step 5: Continue until complete
```

### Autoregressive Generation

LLMs generate text **one token at a time**:
- Each token depends on previous tokens
- Creates coherent, context-aware text
- Can be slow for long outputs

## 🧠 Understanding vs Pattern Matching

### Important Distinction

LLMs don't "understand" like humans:
- They recognize patterns
- They predict based on training data
- They don't have true comprehension

### Why This Matters

- LLMs can be wrong
- They may not "know" what they're saying
- They're very good at seeming to understand

## 📊 Model Components

### Layers

LLMs have multiple **layers**:
- Each layer processes information
- Deeper layers understand more complex patterns
- More layers = more capacity (usually)

### Parameters

**Parameters** are the "knowledge" stored:
- GPT-3: 175 billion parameters
- GPT-4: Estimated 1+ trillion parameters
- More parameters = more knowledge (usually)

### Context Window

**Context window** = maximum input/output:
- GPT-4: 128K tokens
- Claude 3.5: 200K tokens
- Larger context = can handle longer inputs

## 🔄 Inference vs Training

### Training

- Happens once (or periodically)
- Requires massive computing power
- Takes weeks or months
- Creates the model

### Inference

- Happens every time you use the model
- Much faster than training
- Uses the trained model
- What you experience when chatting

## 🎨 Temperature and Sampling

### Temperature

Controls randomness:
- **Low (0-0.3)**: Deterministic, focused
- **Medium (0.5-0.7)**: Balanced
- **High (0.8-1.0)**: Creative, varied

### Top-p (Nucleus Sampling)

Controls diversity:
- Limits choices to most likely tokens
- Balances quality and variety

## 📋 Module 2 Exercises

### Exercise 1: Tokenization
1. Write a sentence
2. Try to break it into tokens (estimate)
3. Use a tokenizer tool to see actual tokens
4. Compare your estimate with reality

### Exercise 2: Generation Process
1. Give an LLM a short prompt
2. Ask it to explain its thinking (if possible)
3. Observe how it generates the response
4. Notice the step-by-step nature

### Exercise 3: Temperature Experiment
1. Ask the same question with temperature 0
2. Ask again with temperature 1
3. Compare the responses
4. Note differences in creativity/consistency

## 🔗 Additional Resources

- [Attention Is All You Need (Original Paper)](https://arxiv.org/abs/1706.03762)
- [The Illustrated Transformer](http://jalammar.github.io/illustrated-transformer/)
- [How GPT Works](https://www.youtube.com/watch?v=wjZofJX0n4Y)

## ✅ Module 2 Checklist

Before moving to Module 3, ensure you can:

- [ ] Explain basic LLM architecture
- [ ] Understand what tokens are
- [ ] Know what embeddings do
- [ ] Understand the attention mechanism
- [ ] Know the difference between training and inference
- [ ] Understand how text generation works

---

**Next Module**: [Module 3: Types of LLMs](../03-types-of-llms/README.md)

