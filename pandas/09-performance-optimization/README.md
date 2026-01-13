# Module 9: Pandas Performance Optimization

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Understand Pandas performance characteristics
- Optimize data types for memory
- Use vectorized operations
- Optimize groupby operations
- Profile Pandas code
- Apply performance best practices

## ⚡ Vectorization vs Iteration

### The Performance Difference

```python
import pandas as pd
import numpy as np
import time

df = pd.DataFrame({'A': np.random.randn(1000000), 'B': np.random.randn(1000000)})

# ❌ Slow: Iteration
start = time.time()
result = []
for idx, row in df.iterrows():
    result.append(row['A'] * row['B'])
slow_time = time.time() - start

# ✅ Fast: Vectorization
start = time.time()
result = df['A'] * df['B']
fast_time = time.time() - start

print(f"Iteration: {slow_time:.4f}s, Vectorization: {fast_time:.4f}s")
# Vectorization is typically 100-1000x faster!
```

### Avoid Iteration

```python
# ❌ Slow: iterrows()
for idx, row in df.iterrows():
    df.loc[idx, 'new_col'] = row['A'] * 2

# ❌ Slow: itertuples()
for row in df.itertuples():
    df.loc[row.Index, 'new_col'] = row.A * 2

# ✅ Fast: Vectorized
df['new_col'] = df['A'] * 2

# ✅ Fast: apply() for complex operations
df['new_col'] = df.apply(lambda row: row['A'] * 2 if row['B'] > 0 else 0, axis=1)
```

## 💾 Memory Optimization

### Optimize Data Types

```python
# Check memory usage
df.info(memory_usage='deep')

# Default: int64 (8 bytes)
df = pd.DataFrame({'A': [1, 2, 3, 4, 5]})
print(df['A'].dtype)  # int64
print(df.memory_usage(deep=True))

# Optimize: int32 (4 bytes) or int8 (1 byte)
df['A'] = df['A'].astype('int32')  # 50% reduction
df['A'] = df['A'].astype('int8')   # 87.5% reduction

# For floats
df['B'] = df['B'].astype('float32')  # Instead of float64
```

### Use Categorical for Strings

```python
# ❌ Memory intensive: object dtype
df = pd.DataFrame({'category': ['A', 'B', 'C'] * 10000})
print(df.memory_usage(deep=True))  # Large

# ✅ Memory efficient: categorical
df['category'] = df['category'].astype('category')
print(df.memory_usage(deep=True))  # Much smaller

# Also faster for operations
df.groupby('category').sum()  # Faster with categorical
```

### Downcast Numeric Types

```python
# Automatically downcast
df['A'] = pd.to_numeric(df['A'], downcast='integer')
df['B'] = pd.to_numeric(df['B'], downcast='float')
```

## 🚀 Optimizing Operations

### Use NumPy for Numeric Operations

```python
# ✅ Fast: NumPy operations
result = np.sum(df['A'].values)  # Convert to NumPy array first

# ❌ Slower: Pandas operations on large arrays
result = df['A'].sum()  # Still fast, but NumPy can be faster for pure numeric
```

### Efficient Filtering

```python
# ✅ Fast: Boolean indexing
df[df['A'] > 0]

# ✅ Fast: Query method
df.query('A > 0')

# ❌ Slower: apply with lambda
df[df.apply(lambda row: row['A'] > 0, axis=1)]
```

### Efficient String Operations

```python
# ✅ Fast: Vectorized string methods
df['text'].str.upper()
df['text'].str.contains('pattern')

# ❌ Slow: apply with Python string methods
df['text'].apply(lambda x: x.upper())
```

## 📊 Optimizing GroupBy

### Pre-filter Before GroupBy

```python
# ✅ Filter first, then group
df[df['value'] > 0].groupby('category').sum()

# ❌ Group everything, then filter
df.groupby('category').sum()[df.groupby('category').sum()['value'] > 0]
```

### Use Categorical for GroupBy Keys

```python
# Convert to categorical before groupby
df['category'] = df['category'].astype('category')
df.groupby('category').sum()  # Faster
```

### Avoid Multiple GroupBy Calls

```python
# ❌ Multiple groupby calls
mean = df.groupby('category')['value'].mean()
sum = df.groupby('category')['value'].sum()

# ✅ Single groupby with multiple aggregations
result = df.groupby('category')['value'].agg(['mean', 'sum'])
```

## 🔍 Profiling Pandas Code

### Using timeit

```python
import timeit

# Time a single operation
time = timeit.timeit(
    "df.groupby('category').sum()",
    setup="import pandas as pd; import numpy as np; df = pd.DataFrame({'category': np.random.choice(['A', 'B', 'C'], 10000), 'value': np.random.randn(10000)})",
    number=100
)
print(f"Average time: {time/100:.6f}s")
```

### Using line_profiler

```python
# Install: pip install line_profiler
# Use: kernprof -l script.py

@profile
def my_function():
    df = pd.DataFrame(...)
    result = df.groupby('category').sum()
    return result
```

### Using cProfile

```python
import cProfile

def process_data():
    df = pd.read_csv('large_file.csv')
    result = df.groupby('category').sum()
    return result

cProfile.run('process_data()')
```

## 🎯 Best Practices

### Reading Large Files

```python
# ✅ Read in chunks
chunk_size = 10000
chunks = []
for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
    processed_chunk = process(chunk)
    chunks.append(processed_chunk)
df = pd.concat(chunks, ignore_index=True)

# ✅ Specify dtypes when reading
dtypes = {'col1': 'int32', 'col2': 'float32', 'col3': 'category'}
df = pd.read_csv('file.csv', dtype=dtypes)

# ✅ Use specific columns
df = pd.read_csv('file.csv', usecols=['col1', 'col2', 'col3'])
```

### Efficient Merging

```python
# ✅ Use categorical for merge keys
df1['key'] = df1['key'].astype('category')
df2['key'] = df2['key'].astype('category')
result = pd.merge(df1, df2, on='key')

# ✅ Sort before merge (if applicable)
df1 = df1.sort_values('key')
df2 = df2.sort_values('key')
result = pd.merge(df1, df2, on='key')
```

### Avoid Chained Indexing

```python
# ❌ Slow: Chained indexing
df[df['A'] > 0]['B'] = 1  # Creates copy, then assignment fails

# ✅ Fast: Use loc
df.loc[df['A'] > 0, 'B'] = 1
```

## 📊 Memory Management

### Release Memory

```python
# Delete large DataFrames when done
del large_df
import gc
gc.collect()
```

### Use Views When Possible

```python
# ✅ View (no copy)
subset = df[['A', 'B']]  # View if possible

# Only copy when necessary
subset = df[['A', 'B']].copy()  # Explicit copy
```

## 📋 Module 9 Exercises

### Exercise 1: Memory Optimization
1. Analyze memory usage of a DataFrame
2. Optimize data types
3. Convert strings to categorical
4. Measure memory savings

### Exercise 2: Performance Comparison
1. Compare iteration vs vectorization
2. Profile different approaches
3. Optimize the slowest operations

### Exercise 3: Large File Processing
1. Read a large file in chunks
2. Process chunks efficiently
3. Combine results

## 🔗 Additional Resources

- [Pandas Performance](https://pandas.pydata.org/docs/user_guide/enhancingperf.html)
- [Pandas Memory Usage](https://pandas.pydata.org/docs/user_guide/scale.html)
- [Profiling Python Code](https://docs.python.org/3/library/profile.html)

## ✅ Module 9 Checklist

Before moving to Module 10, ensure you can:

- [ ] Understand performance differences between methods
- [ ] Optimize data types for memory
- [ ] Use vectorized operations effectively
- [ ] Optimize groupby operations
- [ ] Profile Pandas code
- [ ] Apply performance best practices

---

**Next Module**: [Module 10: Best Practices](../10-best-practices/README.md)

