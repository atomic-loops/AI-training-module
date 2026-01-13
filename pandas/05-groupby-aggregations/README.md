# Module 5: GroupBy & Aggregations

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Use groupby operations effectively
- Apply aggregation functions
- Perform multi-level grouping
- Use transform and apply functions
- Filter groups based on conditions
- Understand groupby best practices

## 🔄 Basic GroupBy

### Simple Grouping

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    'Category': ['A', 'B', 'A', 'B', 'A', 'B'],
    'Value': [10, 20, 30, 40, 50, 60],
    'Count': [1, 2, 3, 4, 5, 6]
})

# Group by single column
grouped = df.groupby('Category')

# Apply aggregation
grouped.sum()
grouped.mean()
grouped.count()
grouped.max()
grouped.min()
```

### Common Aggregations

```python
# Single aggregation
df.groupby('Category')['Value'].sum()
df.groupby('Category')['Value'].mean()

# Multiple aggregations
df.groupby('Category')['Value'].agg(['sum', 'mean', 'std'])

# Different aggregations for different columns
df.groupby('Category').agg({
    'Value': 'sum',
    'Count': 'mean'
})
```

## 📊 Advanced Aggregations

### Custom Aggregation Functions

```python
# Custom function
def range_func(x):
    return x.max() - x.min()

df.groupby('Category')['Value'].agg(range_func)

# Multiple custom functions
df.groupby('Category')['Value'].agg(['sum', range_func, 'mean'])

# Named aggregations
df.groupby('Category').agg(
    total=('Value', 'sum'),
    average=('Value', 'mean'),
    count=('Count', 'count')
)
```

### Multiple Aggregations

```python
# All at once
df.groupby('Category')['Value'].agg(['sum', 'mean', 'std', 'min', 'max'])

# With custom names
df.groupby('Category')['Value'].agg([
    ('total', 'sum'),
    ('average', 'mean'),
    ('std_dev', 'std')
])
```

## 🎯 Multi-Level Grouping

### Grouping by Multiple Columns

```python
df = pd.DataFrame({
    'Category': ['A', 'A', 'B', 'B', 'A', 'B'],
    'Subcategory': ['X', 'Y', 'X', 'Y', 'X', 'Y'],
    'Value': [10, 20, 30, 40, 50, 60]
})

# Group by multiple columns
df.groupby(['Category', 'Subcategory']).sum()

# Access specific group
grouped = df.groupby(['Category', 'Subcategory'])
grouped.get_group(('A', 'X'))
```

### Hierarchical Indexing

```python
# Result has MultiIndex
result = df.groupby(['Category', 'Subcategory']).sum()

# Reset index
result.reset_index()

# Flatten column names
result.columns = ['_'.join(col).strip() for col in result.columns.values]
```

## 🔧 Transform and Apply

### Transform (Same Shape)

```python
# Transform returns same shape as original
df['Value_mean'] = df.groupby('Category')['Value'].transform('mean')

# Custom transform
def normalize(x):
    return (x - x.mean()) / x.std()

df['Value_normalized'] = df.groupby('Category')['Value'].transform(normalize)
```

### Apply (Flexible)

```python
# Apply custom function to each group
def top_n(group, n=2):
    return group.nlargest(n)

df.groupby('Category').apply(top_n, n=2)

# Apply with multiple arguments
def custom_func(group, multiplier):
    return group * multiplier

df.groupby('Category')['Value'].apply(custom_func, multiplier=2)
```

## 🔍 Filtering Groups

### Filter Based on Group Properties

```python
# Filter groups by size
df.groupby('Category').filter(lambda x: len(x) > 2)

# Filter groups by aggregate value
df.groupby('Category').filter(lambda x: x['Value'].sum() > 50)

# Filter groups by condition
df.groupby('Category').filter(lambda x: x['Value'].mean() > 30)
```

## 📈 GroupBy with Time Series

### Time-Based Grouping

```python
# Create time series data
df = pd.DataFrame({
    'date': pd.date_range('2023-01-01', periods=100, freq='D'),
    'value': np.random.randn(100),
    'category': np.random.choice(['A', 'B'], 100)
})

# Group by time periods
df.groupby(pd.Grouper(key='date', freq='M')).sum()  # Monthly
df.groupby(pd.Grouper(key='date', freq='W')).sum()  # Weekly

# Group by category and time
df.groupby(['category', pd.Grouper(key='date', freq='M')]).sum()
```

## 🎨 Pivot Tables

### Creating Pivot Tables

```python
# Simple pivot table
df.pivot_table(values='Value', index='Category', columns='Subcategory', aggfunc='sum')

# Multiple aggregations
df.pivot_table(values='Value', index='Category', aggfunc=['sum', 'mean', 'count'])

# Multiple values
df.pivot_table(values=['Value', 'Count'], index='Category', aggfunc='sum')

# With margins
df.pivot_table(values='Value', index='Category', aggfunc='sum', margins=True)
```

## 🔄 Cross Tabulation

### Crosstab

```python
# Create crosstab
pd.crosstab(df['Category'], df['Subcategory'])

# With values
pd.crosstab(df['Category'], df['Subcategory'], values=df['Value'], aggfunc='sum')

# Normalize
pd.crosstab(df['Category'], df['Subcategory'], normalize=True)  # Proportions
pd.crosstab(df['Category'], df['Subcategory'], normalize='index')  # Row proportions
```

## 📊 Best Practices

### Performance Tips

```python
# ✅ Select columns before groupby
df[['Category', 'Value']].groupby('Category').sum()

# ✅ Use categorical for groupby keys (faster)
df['Category'] = df['Category'].astype('category')
df.groupby('Category').sum()

# ✅ Use as_index=False for cleaner output
df.groupby('Category', as_index=False).sum()
```

### Common Patterns

```python
# Pattern 1: Group, aggregate, reset index
result = df.groupby('Category').agg({'Value': 'sum'}).reset_index()

# Pattern 2: Group, transform, add column
df['group_mean'] = df.groupby('Category')['Value'].transform('mean')

# Pattern 3: Group, filter, continue
filtered = df.groupby('Category').filter(lambda x: len(x) > 1)
```

## 📋 Module 5 Exercises

### Exercise 1: Basic GroupBy
1. Group data by a categorical column
2. Calculate multiple aggregations
3. Use custom aggregation functions

### Exercise 2: Multi-Level Grouping
1. Group by multiple columns
2. Create hierarchical aggregations
3. Flatten the result appropriately

### Exercise 3: Advanced Operations
1. Use transform to add group statistics
2. Filter groups based on conditions
3. Create pivot tables from grouped data

## 🔗 Additional Resources

- [Pandas GroupBy](https://pandas.pydata.org/docs/user_guide/groupby.html)
- [Pandas Pivot Tables](https://pandas.pydata.org/docs/user_guide/reshaping.html#pivot-tables)
- [GroupBy Performance](https://pandas.pydata.org/docs/user_guide/groupby.html#groupby-performance)

## ✅ Module 5 Checklist

Before moving to Module 6, ensure you can:

- [ ] Use basic groupby operations
- [ ] Apply multiple aggregation functions
- [ ] Perform multi-level grouping
- [ ] Use transform and apply effectively
- [ ] Filter groups based on conditions
- [ ] Create pivot tables and crosstabs

---

**Next Module**: [Module 6: Merging & Joining](../06-merging-joining/README.md)

