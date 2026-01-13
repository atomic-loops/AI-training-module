# Module 6: Merging & Joining DataFrames

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Merge DataFrames using different join types
- Join DataFrames on various keys
- Handle duplicate keys and overlapping columns
- Use concat for combining DataFrames
- Understand when to use merge vs concat
- Perform complex data combinations

## 🔗 Basic Merging

### Inner Join

```python
import pandas as pd

df1 = pd.DataFrame({
    'key': ['A', 'B', 'C', 'D'],
    'value1': [1, 2, 3, 4]
})

df2 = pd.DataFrame({
    'key': ['B', 'C', 'D', 'E'],
    'value2': [5, 6, 7, 8]
})

# Inner join (default)
result = pd.merge(df1, df2, on='key')
# Only rows with matching keys in both DataFrames
```

### Left Join

```python
# Left join (keep all from left)
result = pd.merge(df1, df2, on='key', how='left')
# All rows from df1, matched rows from df2
```

### Right Join

```python
# Right join (keep all from right)
result = pd.merge(df1, df2, on='key', how='right')
# All rows from df2, matched rows from df1
```

### Outer Join

```python
# Outer join (keep all from both)
result = pd.merge(df1, df2, on='key', how='outer')
# All rows from both DataFrames
```

## 🔑 Merging on Different Keys

### Different Column Names

```python
df1 = pd.DataFrame({
    'key1': ['A', 'B', 'C'],
    'value1': [1, 2, 3]
})

df2 = pd.DataFrame({
    'key2': ['A', 'B', 'D'],
    'value2': [4, 5, 6]
})

# Merge on different column names
result = pd.merge(df1, df2, left_on='key1', right_on='key2')
```

### Multiple Keys

```python
df1 = pd.DataFrame({
    'key1': ['A', 'B', 'C'],
    'key2': [1, 2, 3],
    'value1': [10, 20, 30]
})

df2 = pd.DataFrame({
    'key1': ['A', 'B', 'C'],
    'key2': [1, 2, 4],
    'value2': [40, 50, 60]
})

# Merge on multiple keys
result = pd.merge(df1, df2, on=['key1', 'key2'])
```

### Index-Based Merging

```python
# Merge on index
result = pd.merge(df1, df2, left_index=True, right_index=True)

# Merge index with column
result = pd.merge(df1, df2, left_on='key', right_index=True)
```

## 🔄 Handling Overlapping Columns

### Suffixes

```python
df1 = pd.DataFrame({
    'key': ['A', 'B', 'C'],
    'value': [1, 2, 3]
})

df2 = pd.DataFrame({
    'key': ['A', 'B', 'C'],
    'value': [4, 5, 6]  # Same column name
})

# Add suffixes to overlapping columns
result = pd.merge(df1, df2, on='key', suffixes=('_left', '_right'))
# Columns: key, value_left, value_right
```

### Indicator Column

```python
# Add indicator showing source of each row
result = pd.merge(df1, df2, on='key', how='outer', indicator=True)
# Adds '_merge' column: 'left_only', 'right_only', 'both'
```

## 📦 Concatenation

### Basic Concatenation

```python
# Concatenate along rows (axis=0)
df1 = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df2 = pd.DataFrame({'A': [5, 6], 'B': [7, 8]})

result = pd.concat([df1, df2])
# Stacks vertically

# Concatenate along columns (axis=1)
result = pd.concat([df1, df2], axis=1)
# Stacks horizontally
```

### Handling Index

```python
# Ignore index (create new sequential index)
result = pd.concat([df1, df2], ignore_index=True)

# Keep original index
result = pd.concat([df1, df2], ignore_index=False)

# Add keys to identify source
result = pd.concat([df1, df2], keys=['first', 'second'])
```

### Different Columns

```python
df1 = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df2 = pd.DataFrame({'A': [5, 6], 'C': [7, 8]})

# Concatenate with different columns
result = pd.concat([df1, df2])  # Missing values filled with NaN
result = pd.concat([df1, df2], join='inner')  # Only common columns
```

## 🔗 Join Method

### DataFrame.join()

```python
# Join on index (default)
df1.join(df2)

# Join on column
df1.set_index('key').join(df2.set_index('key'))

# Join types
df1.join(df2, how='left')
df1.join(df2, how='right')
df1.join(df2, how='outer')
df1.join(df2, how='inner')
```

## 🎯 Advanced Merging

### Merge with Multiple DataFrames

```python
# Merge multiple DataFrames
df1 = pd.DataFrame({'key': ['A', 'B'], 'value1': [1, 2]})
df2 = pd.DataFrame({'key': ['A', 'B'], 'value2': [3, 4]})
df3 = pd.DataFrame({'key': ['A', 'B'], 'value3': [5, 6]})

# Chain merges
result = df1.merge(df2, on='key').merge(df3, on='key')

# Or use reduce
from functools import reduce
result = reduce(lambda left, right: pd.merge(left, right, on='key'), [df1, df2, df3])
```

### Merge with Validation

```python
# Validate merge (raises error if duplicates)
result = pd.merge(df1, df2, on='key', validate='one_to_one')
result = pd.merge(df1, df2, on='key', validate='one_to_many')
result = pd.merge(df1, df2, on='key', validate='many_to_one')
result = pd.merge(df1, df2, on='key', validate='many_to_many')
```

## 📊 Practical Examples

### Combining Sales Data

```python
# Sales by region
sales = pd.DataFrame({
    'region': ['North', 'South', 'East', 'West'],
    'sales': [1000, 2000, 1500, 1800]
})

# Targets by region
targets = pd.DataFrame({
    'region': ['North', 'South', 'East', 'West'],
    'target': [1200, 2200, 1600, 2000]
})

# Merge to compare
comparison = pd.merge(sales, targets, on='region')
comparison['difference'] = comparison['sales'] - comparison['target']
```

### Combining Time Series

```python
# Daily sales
daily = pd.DataFrame({
    'date': pd.date_range('2023-01-01', periods=5),
    'sales': [100, 200, 150, 180, 220]
})

# Daily costs
costs = pd.DataFrame({
    'date': pd.date_range('2023-01-01', periods=5),
    'cost': [50, 100, 75, 90, 110]
})

# Merge and calculate profit
merged = pd.merge(daily, costs, on='date')
merged['profit'] = merged['sales'] - merged['cost']
```

## 🎨 Best Practices

### Performance Tips

```python
# ✅ Use categorical for merge keys (faster)
df1['key'] = df1['key'].astype('category')
df2['key'] = df2['key'].astype('category')
result = pd.merge(df1, df2, on='key')

# ✅ Set index before merge if merging on index
df1 = df1.set_index('key')
df2 = df2.set_index('key')
result = df1.join(df2)

# ✅ Use merge instead of concat for joins
# Merge is optimized for database-style joins
```

### When to Use What

- **merge()**: Database-style joins on keys
- **join()**: Quick joins on index
- **concat()**: Stacking DataFrames (same structure)
- **append()**: Adding rows (deprecated, use concat)

## 📋 Module 6 Exercises

### Exercise 1: Basic Merging
1. Create two DataFrames with common keys
2. Perform inner, left, right, and outer joins
3. Compare the results

### Exercise 2: Complex Merging
1. Merge on multiple keys
2. Handle overlapping column names
3. Use indicator to track merge source

### Exercise 3: Data Combination
1. Combine multiple DataFrames using merge
2. Use concat to stack similar DataFrames
3. Create a final combined dataset

## 🔗 Additional Resources

- [Pandas Merging](https://pandas.pydata.org/docs/user_guide/merging.html)
- [Pandas Concat](https://pandas.pydata.org/docs/user_guide/merging.html#concatenating-objects)
- [SQL-style Joins](https://pandas.pydata.org/docs/user_guide/merging.html#database-style-dataframe-or-named-series-joining-merging)

## ✅ Module 6 Checklist

Before moving to Module 7, ensure you can:

- [ ] Perform different types of joins (inner, left, right, outer)
- [ ] Merge on single and multiple keys
- [ ] Handle overlapping columns with suffixes
- [ ] Use concat for combining DataFrames
- [ ] Choose appropriate method (merge vs concat)
- [ ] Combine multiple DataFrames effectively

---

**Next Module**: [Module 7: Time Series](../07-time-series/README.md)

