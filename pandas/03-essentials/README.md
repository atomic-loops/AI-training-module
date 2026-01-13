# Module 3: Pandas Essentials

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Create Series and DataFrames
- Load data from various sources
- Perform indexing and selection operations
- Use basic data manipulation methods
- Handle missing data

## 📦 Creating Data Structures

### Creating Series

```python
import pandas as pd

# From a list
s1 = pd.Series([1, 2, 3, 4, 5])
print(s1)

# With custom index
s2 = pd.Series([10, 20, 30], index=['a', 'b', 'c'])
print(s2)

# From a dictionary
data = {'Alice': 25, 'Bob': 30, 'Charlie': 35}
s3 = pd.Series(data)
print(s3)
```

### Creating DataFrames

```python
# From a dictionary
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'London', 'Tokyo']
}
df = pd.DataFrame(data)
print(df)

# From a list of dictionaries
data = [
    {'Name': 'Alice', 'Age': 25, 'City': 'New York'},
    {'Name': 'Bob', 'Age': 30, 'City': 'London'},
    {'Name': 'Charlie', 'Age': 35, 'City': 'Tokyo'}
]
df = pd.DataFrame(data)
print(df)

# With custom index
df = pd.DataFrame(data, index=['a', 'b', 'c'])
print(df)
```

## 📂 Loading Data

### Reading CSV Files

```python
# Basic read
df = pd.read_csv('data.csv')

# With options
df = pd.read_csv('data.csv', 
                 sep=',',           # delimiter
                 header=0,          # row to use as header
                 index_col=0,       # column to use as index
                 nrows=100)         # read only first 100 rows
```

### Reading Excel Files

```python
# Read Excel file
df = pd.read_excel('data.xlsx', sheet_name='Sheet1')

# Read specific sheet
df = pd.read_excel('data.xlsx', sheet_name=0)  # First sheet
```

### Reading JSON Files

```python
df = pd.read_json('data.json')
```

### Reading from URLs

```python
url = 'https://example.com/data.csv'
df = pd.read_csv(url)
```

## 🎯 Indexing and Selection

### Selecting Columns

```python
# Single column (returns Series)
df['Name']

# Multiple columns (returns DataFrame)
df[['Name', 'Age']]

# Using dot notation (limited use)
df.Name
```

### Selecting Rows

```python
# By index label
df.loc[0]           # First row
df.loc[0:2]         # Rows 0 to 2

# By integer position
df.iloc[0]          # First row
df.iloc[0:3]        # Rows 0, 1, 2

# By condition
df[df['Age'] > 25]
df[df['City'] == 'New York']
```

### Selecting Both Rows and Columns

```python
# Using loc (label-based)
df.loc[0, 'Name']              # Single value
df.loc[0:2, ['Name', 'Age']]  # Multiple rows and columns

# Using iloc (position-based)
df.iloc[0, 0]                  # First row, first column
df.iloc[0:3, 0:2]              # First 3 rows, first 2 columns
```

### Boolean Indexing

```python
# Single condition
df[df['Age'] > 25]

# Multiple conditions
df[(df['Age'] > 25) & (df['City'] == 'New York')]
df[(df['Age'] > 30) | (df['City'] == 'London')]

# Using query method
df.query('Age > 25 and City == "New York"')
```

## 🔧 Basic Data Manipulation

### Adding Columns

```python
# Add new column
df['Salary'] = [50000, 60000, 70000]

# Add calculated column
df['Age_Plus_10'] = df['Age'] + 10

# Add column based on condition
df['Senior'] = df['Age'] > 30
```

### Dropping Columns/Rows

```python
# Drop columns
df.drop('City', axis=1)           # Returns new DataFrame
df.drop('City', axis=1, inplace=True)  # Modifies in place

# Drop rows
df.drop(0)                        # Drop row with index 0
df.drop([0, 1])                   # Drop multiple rows
```

### Renaming

```python
# Rename columns
df.rename(columns={'Name': 'Full_Name', 'Age': 'Years'})

# Rename index
df.rename(index={0: 'first', 1: 'second'})
```

## 🧹 Handling Missing Data

### Detecting Missing Data

```python
# Check for missing values
df.isna()           # Boolean DataFrame
df.isnull()         # Same as isna()
df.notna()          # Opposite of isna()

# Count missing values
df.isna().sum()     # Count per column
df.isna().sum().sum()  # Total count
```

### Removing Missing Data

```python
# Drop rows with any missing values
df.dropna()

# Drop rows where all values are missing
df.dropna(how='all')

# Drop columns with missing values
df.dropna(axis=1)

# Drop rows with missing values in specific column
df.dropna(subset=['Age'])
```

### Filling Missing Data

```python
# Fill with specific value
df.fillna(0)

# Fill with forward fill
df.fillna(method='ffill')

# Fill with backward fill
df.fillna(method='bfill')

# Fill with mean
df['Age'].fillna(df['Age'].mean())

# Fill different columns with different values
df.fillna({'Age': df['Age'].mean(), 'Salary': 0})
```

## 📊 Basic Statistics

```python
# Summary statistics
df.describe()

# Individual statistics
df['Age'].mean()
df['Age'].median()
df['Age'].std()
df['Age'].min()
df['Age'].max()
df['Age'].sum()
df['Age'].count()

# Value counts
df['City'].value_counts()

# Unique values
df['City'].unique()
df['City'].nunique()
```

## 📋 Module 3 Exercises

### Exercise 1: DataFrame Creation
1. Create a DataFrame with 5 rows and 4 columns
2. Add a new column to the DataFrame
3. Rename one of the columns

### Exercise 2: Data Selection
Given a DataFrame with columns: Name, Age, City, Salary
1. Select only the Name and Age columns
2. Select rows where Age > 25
3. Select the first 3 rows and first 2 columns

### Exercise 3: Data Cleaning
1. Create a DataFrame with some missing values
2. Count the missing values in each column
3. Fill missing values with appropriate methods
4. Remove rows with missing values in a specific column

## 🔗 Additional Resources

- [Pandas User Guide - Intro to Data Structures](https://pandas.pydata.org/docs/user_guide/dsintro.html)
- [Pandas User Guide - Indexing and Selecting Data](https://pandas.pydata.org/docs/user_guide/indexing.html)
- [Pandas User Guide - Working with Missing Data](https://pandas.pydata.org/docs/user_guide/missing_data.html)

## ✅ Module 3 Checklist

Before moving to advanced topics, ensure you can:

- [ ] Create Series and DataFrames
- [ ] Load data from CSV, Excel, and JSON files
- [ ] Perform various indexing and selection operations
- [ ] Add, remove, and rename columns
- [ ] Detect and handle missing data
- [ ] Calculate basic statistics

---

**Next Steps**: Continue with advanced Pandas topics or move to practical applications

