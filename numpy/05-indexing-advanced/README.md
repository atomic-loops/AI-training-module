# Module 5: Advanced Indexing

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Use fancy indexing effectively
- Apply boolean indexing for complex conditions
- Understand integer array indexing
- Use advanced slicing techniques
- Work with structured arrays

## 🎨 Fancy Indexing

Fancy indexing uses integer arrays to select elements.

### 1D Fancy Indexing

```python
import numpy as np

arr = np.array([10, 20, 30, 40, 50, 60, 70, 80])

# Select specific indices
indices = [1, 3, 5]
result = arr[indices]  # [20 40 60]

# Select in any order
indices = [5, 1, 3, 0]
result = arr[indices]  # [60 20 40 10]

# Select with repetition
indices = [0, 0, 1, 2, 2, 2]
result = arr[indices]  # [10 10 20 30 30 30]
```

### 2D Fancy Indexing

```python
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# Select rows
rows = [0, 2]
result = arr[rows]  # [[1 2 3] [7 8 9]]

# Select specific elements
row_indices = [0, 1, 2]
col_indices = [2, 1, 0]
result = arr[row_indices, col_indices]  # [3 5 7]

# Select subarrays
result = arr[[0, 2], :]  # Rows 0 and 2, all columns
result = arr[:, [0, 2]]  # All rows, columns 0 and 2
```

## 🔍 Boolean Indexing

Boolean indexing uses boolean arrays to select elements.

### Basic Boolean Indexing

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Simple condition
mask = arr > 5
result = arr[mask]  # [6 7 8 9 10]

# Direct boolean indexing
result = arr[arr > 5]  # [6 7 8 9 10]

# Multiple conditions
result = arr[(arr > 3) & (arr < 8)]  # [4 5 6 7]
result = arr[(arr < 3) | (arr > 8)]  # [1 2 9 10]
```

### 2D Boolean Indexing

```python
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# Boolean mask
mask = arr > 5
result = arr[mask]  # [6 7 8 9] - flattened

# Select rows based on condition
mask = arr[:, 0] > 3  # Rows where first column > 3
result = arr[mask]  # [[4 5 6] [7 8 9]]

# Select elements based on condition
result = arr[arr > 5] = -1  # Replace all > 5 with -1
```

### Setting Values with Boolean Indexing

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Set values based on condition
arr[arr > 5] = 0  # Set all > 5 to 0
arr[arr % 2 == 0] = -1  # Set even numbers to -1

# Increment values
arr[arr < 5] += 10  # Add 10 to all < 5
```

## 🔢 Integer Array Indexing

Integer array indexing allows selection of arbitrary elements.

### Combining Integer Arrays

```python
arr = np.array([[1, 2, 3, 4], 
                [5, 6, 7, 8], 
                [9, 10, 11, 12]])

# Select specific elements
rows = np.array([0, 1, 2])
cols = np.array([0, 1, 2])
result = arr[rows, cols]  # [1 6 11] - diagonal elements

# Select rectangular region
rows = np.array([0, 2])
cols = np.array([1, 3])
result = arr[rows[:, np.newaxis], cols]  # 2x2 subarray
```

## 🎯 Advanced Slicing

### Step Slicing

```python
arr = np.array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

# Every other element
arr[::2]  # [0 2 4 6 8]

# Reverse array
arr[::-1]  # [9 8 7 6 5 4 3 2 1 0]

# Every third element, starting from index 1
arr[1::3]  # [1 4 7]
```

### Multi-dimensional Slicing

```python
arr = np.array([[1, 2, 3, 4], 
                [5, 6, 7, 8], 
                [9, 10, 11, 12],
                [13, 14, 15, 16]])

# Select subarray
sub = arr[1:3, 1:3]  # [[6 7] [10 11]]

# Select with steps
sub = arr[::2, ::2]  # [[1 3] [9 11]]

# Select all rows, specific columns
cols = arr[:, [0, 2, 3]]  # Columns 0, 2, 3
```

## 📊 Structured Arrays

Structured arrays allow arrays with different data types per column.

### Creating Structured Arrays

```python
# Define structured dtype
dtype = [('name', 'U10'), ('age', 'i4'), ('weight', 'f4')]

# Create structured array
data = np.array([('Alice', 25, 55.5), 
                 ('Bob', 30, 70.2), 
                 ('Charlie', 35, 80.1)], 
                dtype=dtype)

# Access fields
print(data['name'])    # ['Alice' 'Bob' 'Charlie']
print(data['age'])     # [25 30 35]
print(data[0])         # ('Alice', 25, 55.5)
```

### Indexing Structured Arrays

```python
# Select by field
names = data['name']

# Select by condition
young = data[data['age'] < 30]

# Select multiple fields
subset = data[['name', 'age']]
```

## 🎨 Combining Indexing Methods

```python
arr = np.array([[1, 2, 3, 4], 
                [5, 6, 7, 8], 
                [9, 10, 11, 12]])

# Mix fancy indexing and slicing
result = arr[[0, 2], 1:3]  # Rows 0,2; columns 1-2

# Mix boolean and fancy indexing
mask = arr[:, 0] > 3
result = arr[mask, [0, 2]]  # Selected rows, columns 0,2
```

## 📋 Module 5 Exercises

### Exercise 1: Fancy Indexing
1. Create an array and select elements at indices [0, 2, 4, 6]
2. Select a diagonal from a 2D array using fancy indexing
3. Select a checkerboard pattern from a 2D array

### Exercise 2: Boolean Indexing
1. Filter an array to keep only values between 10 and 50
2. Replace all negative values in an array with 0
3. Select rows from a 2D array where the sum is greater than a threshold

### Exercise 3: Advanced Techniques
1. Create a structured array with name, age, and salary
2. Filter the structured array based on age
3. Combine multiple indexing methods to select complex subsets

## 🔗 Additional Resources

- [NumPy Advanced Indexing](https://numpy.org/doc/stable/user/basics.indexing.html#advanced-indexing)
- [NumPy Structured Arrays](https://numpy.org/doc/stable/user/basics.rec.html)
- [NumPy Indexing Tricks](https://numpy.org/doc/stable/reference/arrays.indexing.html)

## ✅ Module 5 Checklist

Before moving to Module 6, ensure you can:

- [ ] Use fancy indexing to select arbitrary elements
- [ ] Apply boolean indexing with complex conditions
- [ ] Combine different indexing methods
- [ ] Work with structured arrays
- [ ] Set values using advanced indexing

---

**Next Module**: [Module 6: Linear Algebra](../06-linear-algebra/README.md)

