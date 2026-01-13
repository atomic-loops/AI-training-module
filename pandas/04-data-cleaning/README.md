# Module 4: Data Cleaning with Pandas

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Handle missing data effectively
- Remove duplicates
- Fix data type issues
- Clean and standardize text data
- Handle outliers
- Validate and transform data

## 🧹 Handling Missing Data

### Detecting Missing Values

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    'A': [1, 2, np.nan, 4, 5],
    'B': [1.0, 2.0, 3.0, np.nan, 5.0],
    'C': ['a', 'b', None, 'd', 'e']
})

# Check for missing values
df.isna()           # Boolean DataFrame
df.isnull()         # Same as isna()
df.notna()          # Opposite

# Count missing values
df.isna().sum()     # Per column
df.isna().sum().sum()  # Total
df.isna().any()     # Any missing per column
```

### Removing Missing Data

```python
# Drop rows with any missing values
df.dropna()

# Drop rows where all values are missing
df.dropna(how='all')

# Drop columns with missing values
df.dropna(axis=1)

# Drop rows with missing values in specific columns
df.dropna(subset=['A', 'B'])

# Drop if threshold of non-null values not met
df.dropna(thresh=3)  # Keep rows with at least 3 non-null values
```

### Filling Missing Data

```python
# Fill with specific value
df.fillna(0)
df['A'].fillna(0)

# Forward fill
df.fillna(method='ffill')  # or 'pad'
df.fillna(method='bfill')  # Backward fill

# Fill with mean/median/mode
df['A'].fillna(df['A'].mean())
df['A'].fillna(df['A'].median())
df['A'].fillna(df['A'].mode()[0])

# Fill different columns with different values
df.fillna({'A': df['A'].mean(), 'B': 0, 'C': 'unknown'})

# Interpolate
df['A'].interpolate()  # Linear interpolation
```

## 🔄 Removing Duplicates

### Finding Duplicates

```python
# Check for duplicates
df.duplicated()  # Boolean Series

# Check specific columns
df.duplicated(subset=['A', 'B'])

# Count duplicates
df.duplicated().sum()
```

### Removing Duplicates

```python
# Remove duplicate rows
df.drop_duplicates()

# Remove duplicates based on specific columns
df.drop_duplicates(subset=['A', 'B'])

# Keep first or last occurrence
df.drop_duplicates(keep='first')   # Default
df.drop_duplicates(keep='last')
df.drop_duplicates(keep=False)     # Remove all duplicates

# Remove duplicates in place
df.drop_duplicates(inplace=True)
```

## 🔧 Fixing Data Types

### Converting Data Types

```python
# Convert to specific type
df['A'] = df['A'].astype(int)
df['B'] = df['B'].astype(float)
df['C'] = df['C'].astype(str)

# Convert to datetime
df['date'] = pd.to_datetime(df['date'])

# Convert to category (memory efficient)
df['category'] = df['category'].astype('category')

# Convert to numeric (handles errors)
df['A'] = pd.to_numeric(df['A'], errors='coerce')  # Invalid -> NaN
```

### Handling Type Errors

```python
# Find non-numeric values
df['A'] = pd.to_numeric(df['A'], errors='coerce')

# Convert with downcast
df['A'] = pd.to_numeric(df['A'], downcast='integer')  # Use smallest int type
```

## 📝 Text Data Cleaning

### String Operations

```python
# String methods (vectorized)
df['text'].str.lower()
df['text'].str.upper()
df['text'].str.strip()      # Remove whitespace
df['text'].str.lstrip()     # Left strip
df['text'].str.rstrip()     # Right strip

# Replace
df['text'].str.replace('old', 'new')
df['text'].str.replace(r'\d+', '', regex=True)  # Remove digits

# Split and extract
df['text'].str.split(' ')
df['text'].str.extract(r'(\d+)')  # Extract pattern

# Check conditions
df['text'].str.contains('pattern')
df['text'].str.startswith('prefix')
df['text'].str.endswith('suffix')
```

### Standardizing Text

```python
# Remove special characters
df['text'] = df['text'].str.replace(r'[^a-zA-Z0-9\s]', '', regex=True)

# Normalize whitespace
df['text'] = df['text'].str.replace(r'\s+', ' ', regex=True)

# Title case
df['text'] = df['text'].str.title()

# Remove extra spaces
df['text'] = df['text'].str.strip().str.replace(r'\s+', ' ', regex=True)
```

## 🎯 Handling Outliers

### Detecting Outliers

```python
# Using IQR method
Q1 = df['A'].quantile(0.25)
Q3 = df['A'].quantile(0.75)
IQR = Q3 - Q1
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = df[(df['A'] < lower_bound) | (df['A'] > upper_bound)]

# Using Z-score
from scipy import stats
z_scores = np.abs(stats.zscore(df['A']))
outliers = df[z_scores > 3]  # 3 standard deviations
```

### Handling Outliers

```python
# Remove outliers
df_clean = df[(df['A'] >= lower_bound) & (df['A'] <= upper_bound)]

# Cap outliers
df['A'] = df['A'].clip(lower=lower_bound, upper=upper_bound)

# Replace with median
median = df['A'].median()
df.loc[df['A'] > upper_bound, 'A'] = median
df.loc[df['A'] < lower_bound, 'A'] = median
```

## ✅ Data Validation

### Checking Data Quality

```python
# Check for negative values
df[df['A'] < 0]

# Check for values outside range
df[(df['A'] < 0) | (df['A'] > 100)]

# Check for invalid categories
valid_categories = ['A', 'B', 'C']
df[~df['category'].isin(valid_categories)]

# Check data types
df.dtypes

# Check value ranges
df.describe()
```

### Data Transformation

```python
# Normalize values
df['A_normalized'] = (df['A'] - df['A'].min()) / (df['A'].max() - df['A'].min())

# Standardize (z-score)
df['A_standardized'] = (df['A'] - df['A'].mean()) / df['A'].std()

# Log transform
df['A_log'] = np.log(df['A'] + 1)  # +1 to handle zeros

# Binning
df['A_binned'] = pd.cut(df['A'], bins=5)
df['A_binned'] = pd.qcut(df['A'], q=5)  # Quantile-based
```

## 🔄 Reshaping Data

### Pivot and Melt

```python
# Pivot (long to wide)
df_pivot = df.pivot(index='date', columns='category', values='value')

# Melt (wide to long)
df_melt = df.melt(id_vars=['id'], value_vars=['A', 'B', 'C'])

# Pivot table with aggregation
df_pivot = df.pivot_table(values='value', index='date', columns='category', aggfunc='mean')
```

## 📋 Module 4 Exercises

### Exercise 1: Missing Data
1. Load a dataset with missing values
2. Analyze the pattern of missing data
3. Choose appropriate strategy (drop or fill) for each column
4. Implement the cleaning

### Exercise 2: Duplicates and Types
1. Find and remove duplicate rows
2. Convert columns to appropriate data types
3. Handle type conversion errors

### Exercise 3: Text Cleaning
1. Clean text columns (remove special chars, normalize)
2. Extract information from text (dates, numbers, etc.)
3. Standardize text formats

## 🔗 Additional Resources

- [Pandas Missing Data](https://pandas.pydata.org/docs/user_guide/missing_data.html)
- [Pandas Text Data](https://pandas.pydata.org/docs/user_guide/text.html)
- [Data Cleaning Best Practices](https://pandas.pydata.org/docs/user_guide/basics.html#basics-dtypes)

## ✅ Module 4 Checklist

Before moving to Module 5, ensure you can:

- [ ] Detect and handle missing data appropriately
- [ ] Remove and handle duplicates
- [ ] Convert and fix data types
- [ ] Clean and standardize text data
- [ ] Detect and handle outliers
- [ ] Validate and transform data

---

**Next Module**: [Module 5: GroupBy & Aggregations](../05-groupby-aggregations/README.md)

