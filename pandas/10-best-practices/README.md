# Module 10: Pandas Best Practices

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Follow Pandas coding conventions
- Write clean and readable Pandas code
- Avoid common anti-patterns
- Use Pandas idioms effectively
- Write maintainable and efficient code

## 📝 Code Style and Conventions

### Import Convention

```python
# ✅ Standard and expected
import pandas as pd
import numpy as np

# ❌ Non-standard
import pandas
import pandas as p
from pandas import *
```

### Naming Conventions

```python
# ✅ Good: Descriptive names
sales_data = pd.read_csv('sales.csv')
customer_df = pd.DataFrame(...)
monthly_summary = df.groupby('month').sum()

# ❌ Bad: Unclear names
df = pd.read_csv('sales.csv')
df2 = pd.DataFrame(...)
result = df.groupby('month').sum()
```

## 🎯 Pandas Idioms

### Use Vectorized Operations

```python
# ✅ Idiomatic: Vectorized
df['new_col'] = df['A'] * 2
df['filtered'] = df[df['A'] > 0]

# ❌ Anti-pattern: Loop
for idx, row in df.iterrows():
    df.loc[idx, 'new_col'] = row['A'] * 2
```

### Use Method Chaining

```python
# ✅ Idiomatic: Method chaining
result = (df
    .query('value > 0')
    .groupby('category')
    .agg({'value': 'sum', 'count': 'mean'})
    .reset_index()
    .sort_values('value', ascending=False)
)

# ❌ Less readable: Multiple assignments
df_filtered = df[df['value'] > 0]
df_grouped = df_filtered.groupby('category').agg({'value': 'sum', 'count': 'mean'})
df_reset = df_grouped.reset_index()
result = df_reset.sort_values('value', ascending=False)
```

### Use Query for Complex Filters

```python
# ✅ Idiomatic: Query
df.query('A > 0 and B < 10 and category == "X"')

# ❌ Less readable: Boolean indexing
df[(df['A'] > 0) & (df['B'] < 10) & (df['category'] == 'X')]
```

## 🔧 Error Handling

### Validate Inputs

```python
def process_dataframe(df):
    # ✅ Validate input
    if not isinstance(df, pd.DataFrame):
        raise TypeError("Input must be a pandas DataFrame")
    
    if df.empty:
        raise ValueError("DataFrame cannot be empty")
    
    required_columns = ['A', 'B', 'C']
    missing = set(required_columns) - set(df.columns)
    if missing:
        raise ValueError(f"Missing required columns: {missing}")
    
    # Process DataFrame
    return df.groupby('A').sum()
```

### Handle Missing Data Explicitly

```python
# ✅ Explicit handling
if df['A'].isna().any():
    df['A'] = df['A'].fillna(df['A'].mean())

# Or raise error
if df['A'].isna().any():
    raise ValueError("Column A contains missing values")
```

## 📊 Documentation

### Docstrings

```python
def calculate_monthly_sales(df):
    """
    Calculate monthly sales totals from transaction data.
    
    Parameters
    ----------
    df : pd.DataFrame
        DataFrame with columns 'date', 'amount', and 'category'
        
    Returns
    -------
    pd.DataFrame
        DataFrame with monthly sales totals
        
    Examples
    --------
    >>> df = pd.DataFrame({
    ...     'date': pd.date_range('2023-01-01', periods=10, freq='D'),
    ...     'amount': [100, 200, 150, 300, 250, 180, 220, 190, 210, 240]
    ... })
    >>> result = calculate_monthly_sales(df)
    >>> result.shape[0] > 0
    True
    """
    df['month'] = pd.to_datetime(df['date']).dt.to_period('M')
    return df.groupby('month')['amount'].sum().reset_index()
```

## 🎨 Code Organization

### Separate Concerns

```python
# ✅ Good: Separate functions
def load_data(filepath):
    """Load and validate data."""
    df = pd.read_csv(filepath)
    validate_data(df)
    return df

def clean_data(df):
    """Clean the data."""
    df = df.dropna()
    df = df.drop_duplicates()
    return df

def process_data(df):
    """Process the data."""
    return df.groupby('category').sum()

# Usage
df = load_data('data.csv')
df_clean = clean_data(df)
result = process_data(df_clean)
```

### Use Functions for Repeated Operations

```python
# ✅ Good: Reusable function
def normalize_column(df, col):
    """Normalize column to [0, 1] range."""
    min_val = df[col].min()
    max_val = df[col].max()
    return (df[col] - min_val) / (max_val - min_val)

df['A_norm'] = normalize_column(df, 'A')
df['B_norm'] = normalize_column(df, 'B')

# ❌ Bad: Repeated code
df['A_norm'] = (df['A'] - df['A'].min()) / (df['A'].max() - df['A'].min())
df['B_norm'] = (df['B'] - df['B'].min()) / (df['B'].max() - df['B'].min())
```

## 🚫 Common Anti-patterns

### Don't Modify During Iteration

```python
# ❌ Bad: Modifying during iteration
for idx, row in df.iterrows():
    if row['value'] > 100:
        df.loc[idx, 'flag'] = 'high'

# ✅ Good: Vectorized assignment
df['flag'] = df['value'].apply(lambda x: 'high' if x > 100 else 'low')
# Or
df.loc[df['value'] > 100, 'flag'] = 'high'
```

### Don't Use Chained Indexing

```python
# ❌ Bad: Chained indexing
df[df['A'] > 0]['B'] = 1  # May not work as expected

# ✅ Good: Use loc
df.loc[df['A'] > 0, 'B'] = 1
```

### Don't Mix Data Types Unnecessarily

```python
# ❌ Bad: Mixed types in single column
df['mixed'] = [1, 'text', 3.5, None]

# ✅ Good: Consistent types
df['numbers'] = [1, 2, 3, 4]
df['text'] = ['a', 'b', 'c', 'd']
```

## ✅ Type Hints (Python 3.5+)

```python
from typing import List, Optional
import pandas as pd

def process_data(
    df: pd.DataFrame,
    columns: List[str],
    threshold: float = 0.5
) -> pd.DataFrame:
    """Process DataFrame and return result."""
    return df[columns].query(f'value > {threshold}')

def get_summary(df: pd.DataFrame) -> Optional[pd.Series]:
    """Get summary statistics."""
    if df.empty:
        return None
    return df.describe()
```

## 🧪 Testing

### Unit Tests

```python
import unittest
import pandas as pd
import numpy as np

class TestDataProcessing(unittest.TestCase):
    def setUp(self):
        self.df = pd.DataFrame({
            'A': [1, 2, 3, 4, 5],
            'B': [10, 20, 30, 40, 50]
        })
    
    def test_groupby_sum(self):
        result = self.df.groupby('A').sum()
        self.assertEqual(result.loc[1, 'B'], 10)
    
    def test_filter(self):
        filtered = self.df[self.df['A'] > 3]
        self.assertEqual(len(filtered), 2)
    
    def test_calculation(self):
        self.df['C'] = self.df['A'] * self.df['B']
        self.assertEqual(self.df.loc[0, 'C'], 10)
```

## 📋 Module 10 Exercises

### Exercise 1: Code Review
1. Review Pandas code and identify anti-patterns
2. Refactor code to follow best practices
3. Add proper documentation

### Exercise 2: Write Clean Code
1. Write a function following Pandas best practices
2. Add type hints and docstrings
3. Include error handling

### Exercise 3: Testing
1. Write unit tests for Pandas functions
2. Test edge cases and error conditions
3. Verify vectorized operations

## 🔗 Additional Resources

- [Pandas Style Guide](https://pandas.pydata.org/docs/development/contributing.html)
- [PEP 8 Style Guide](https://pep8.org/)
- [Pandas Documentation Standards](https://pandas.pydata.org/docs/development/contributing_docstring.html)

## ✅ Module 10 Checklist

Before moving to Module 11, ensure you can:

- [ ] Follow Pandas coding conventions
- [ ] Write idiomatic Pandas code
- [ ] Avoid common anti-patterns
- [ ] Document code properly
- [ ] Write testable Pandas code
- [ ] Handle errors appropriately
- [ ] Organize code effectively

---

**Next Module**: [Module 11: Common Pitfalls](../11-pitfalls/README.md)

