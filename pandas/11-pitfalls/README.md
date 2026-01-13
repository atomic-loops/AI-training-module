# Module 11: Common Pitfalls & Solutions

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Identify common Pandas mistakes
- Understand why these mistakes occur
- Apply correct solutions
- Avoid performance pitfalls
- Debug Pandas issues effectively

## ⚠️ Pitfall 1: SettingWithCopyWarning

### The Problem

```python
import pandas as pd

df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6]})

# ⚠️ Warning: SettingWithCopyWarning
subset = df[df['A'] > 1]
subset['C'] = 10  # Warning! May not modify original
```

### The Solution

```python
# ✅ Explicit copy
subset = df[df['A'] > 1].copy()
subset['C'] = 10  # Safe, works on copy

# ✅ Or modify original directly
df.loc[df['A'] > 1, 'C'] = 10  # Modifies original
```

## ⚠️ Pitfall 2: Chained Indexing

### The Problem

```python
# ❌ Chained indexing - may not work
df[df['A'] > 1]['B'] = 10  # SettingWithCopyWarning
```

### The Solution

```python
# ✅ Use loc for assignment
df.loc[df['A'] > 1, 'B'] = 10

# ✅ Or use query
df.loc[df.query('A > 1').index, 'B'] = 10
```

## ⚠️ Pitfall 3: Modifying During Iteration

### The Problem

```python
# ❌ Slow and may not work correctly
for idx, row in df.iterrows():
    if row['A'] > 1:
        df.loc[idx, 'B'] = row['A'] * 2
```

### The Solution

```python
# ✅ Vectorized operation
df.loc[df['A'] > 1, 'B'] = df.loc[df['A'] > 1, 'A'] * 2

# ✅ Or use apply
df.loc[df['A'] > 1, 'B'] = df.loc[df['A'] > 1, 'A'].apply(lambda x: x * 2)
```

## ⚠️ Pitfall 4: NaN Comparison Issues

### The Problem

```python
# ❌ NaN comparisons always return False
df[df['A'] == np.nan]  # Empty! NaN != NaN
df[df['A'] != np.nan]  # All rows! NaN != NaN
```

### The Solution

```python
# ✅ Use isna() or notna()
df[df['A'].isna()]
df[df['A'].notna()]

# ✅ Or use pd.isna()
df[pd.isna(df['A'])]
```

## ⚠️ Pitfall 5: String Operations on Non-Strings

### The Problem

```python
# ❌ Error if column contains non-strings
df['text'].str.upper()  # AttributeError if mixed types
```

### The Solution

```python
# ✅ Convert to string first
df['text'] = df['text'].astype(str)
df['text'].str.upper()

# ✅ Or handle mixed types
df['text'] = df['text'].apply(lambda x: str(x).upper() if pd.notna(x) else x)
```

## ⚠️ Pitfall 6: Memory Issues with Large DataFrames

### The Problem

```python
# ❌ Creating unnecessary copies
large_df = pd.read_csv('large_file.csv')
copy1 = large_df.copy()  # Huge memory copy!
copy2 = large_df.copy()  # Another huge copy!
```

### The Solution

```python
# ✅ Use views when possible
subset = large_df[['col1', 'col2']]  # View, not copy

# ✅ Only copy when necessary
copy = large_df.copy()  # Only when you need independent data

# ✅ Process in chunks
for chunk in pd.read_csv('large_file.csv', chunksize=10000):
    process(chunk)
```

## ⚠️ Pitfall 7: Wrong Data Types

### The Problem

```python
# ❌ Using object dtype for numeric data
df = pd.DataFrame({'numbers': ['1', '2', '3']})  # Strings, not numbers!
df['numbers'].sum()  # Concatenates: '123' instead of 6
```

### The Solution

```python
# ✅ Convert to numeric
df['numbers'] = pd.to_numeric(df['numbers'])
df['numbers'].sum()  # Now works: 6

# ✅ Or specify dtype when reading
df = pd.read_csv('file.csv', dtype={'numbers': 'int64'})
```

## ⚠️ Pitfall 8: Index Confusion

### The Problem

```python
# ❌ Resetting index loses information
df = df.reset_index()  # Old index becomes column, may cause confusion
```

### The Solution

```python
# ✅ Be explicit about index
df = df.reset_index(drop=True)  # Drop old index

# ✅ Or keep old index as column with name
df = df.reset_index(names='old_index')
```

## ⚠️ Pitfall 9: Merge Key Issues

### The Problem

```python
# ❌ Merge fails if keys have different types
df1 = pd.DataFrame({'key': [1, 2, 3]})  # int
df2 = pd.DataFrame({'key': ['1', '2', '3']})  # string
result = pd.merge(df1, df2, on='key')  # No matches!
```

### The Solution

```python
# ✅ Ensure matching types
df2['key'] = df2['key'].astype(int)
result = pd.merge(df1, df2, on='key')  # Now works

# ✅ Or convert when reading
df2 = pd.read_csv('file.csv', dtype={'key': 'int64'})
```

## ⚠️ Pitfall 10: Time Zone Issues

### The Problem

```python
# ❌ Mixing timezone-aware and naive datetimes
df1 = pd.DataFrame({'date': pd.date_range('2023-01-01', periods=5, tz='UTC')})
df2 = pd.DataFrame({'date': pd.date_range('2023-01-01', periods=5)})  # No tz
# Operations may fail or give unexpected results
```

### The Solution

```python
# ✅ Make timezones consistent
df2['date'] = df2['date'].dt.tz_localize('UTC')
# Or
df1['date'] = df1['date'].dt.tz_localize(None)  # Remove timezone
```

## 🔍 Debugging Tips

### Check DataFrame Properties

```python
# Debug information
print(f"Shape: {df.shape}")
print(f"Columns: {df.columns.tolist()}")
print(f"Dtypes:\n{df.dtypes}")
print(f"Memory usage:\n{df.memory_usage(deep=True)}")
print(f"Index: {df.index}")
print(f"Has duplicates: {df.duplicated().any()}")
print(f"Has NaN: {df.isna().any().any()}")
```

### Common Error Messages

```python
# KeyError: Column not found
# Solution: Check column names with df.columns

# ValueError: Cannot convert
# Solution: Check data types, use appropriate conversion

# SettingWithCopyWarning
# Solution: Use .copy() or .loc for assignment

# MemoryError
# Solution: Process in chunks, optimize dtypes
```

## 📋 Module 11 Exercises

### Exercise 1: Identify Pitfalls
1. Review code snippets and identify pitfalls
2. Explain why each is a problem
3. Provide corrected versions

### Exercise 2: Fix Common Errors
1. Fix SettingWithCopyWarning issues
2. Correct chained indexing problems
3. Handle NaN and type issues

### Exercise 3: Debug Practice
1. Write code with intentional pitfalls
2. Debug and fix the issues
3. Verify solutions work correctly

## 🔗 Additional Resources

- [Pandas Gotchas](https://pandas.pydata.org/docs/user_guide/gotchas.html)
- [Pandas Troubleshooting](https://pandas.pydata.org/docs/user_guide/troubleshooting.html)
- [Common Pandas Errors](https://pandas.pydata.org/docs/user_guide/index.html)

## ✅ Module 11 Checklist

Before completing the Pandas playbook, ensure you can:

- [ ] Identify common Pandas pitfalls
- [ ] Understand SettingWithCopyWarning
- [ ] Fix chained indexing issues
- [ ] Handle NaN and type issues
- [ ] Debug Pandas code effectively
- [ ] Avoid memory and performance pitfalls

---

**Congratulations!** You've completed the Pandas playbook. Continue practicing and exploring advanced topics!

