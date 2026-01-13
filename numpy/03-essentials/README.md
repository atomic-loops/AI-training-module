# Module 3: NumPy Essentials

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Create NumPy arrays using various methods
- Understand array attributes and data types
- Perform indexing and slicing operations
- Use basic array operations and functions
- Work with multi-dimensional arrays

## 📦 Creating Arrays

### From Python Lists

```python
import numpy as np

# 1D array
arr1d = np.array([1, 2, 3, 4, 5])
print(arr1d)  # [1 2 3 4 5]

# 2D array
arr2d = np.array([[1, 2, 3], [4, 5, 6]])
print(arr2d)
# [[1 2 3]
#  [4 5 6]]

# 3D array
arr3d = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
print(arr3d.shape)  # (2, 2, 2)
```

### Using Built-in Functions

```python
# Zeros
zeros = np.zeros((3, 4))  # 3x4 array of zeros

# Ones
ones = np.ones((2, 3))    # 2x3 array of ones

# Full (fill with specific value)
full = np.full((2, 2), 7)  # 2x2 array filled with 7

# Identity matrix
identity = np.eye(3)       # 3x3 identity matrix

# Range
range_arr = np.arange(0, 10, 2)  # [0 2 4 6 8]

# Linspace (evenly spaced)
linspace_arr = np.linspace(0, 1, 5)  # [0.   0.25 0.5  0.75 1.  ]

# Random
random_arr = np.random.rand(3, 3)  # 3x3 random array (0-1)
random_int = np.random.randint(0, 10, (3, 3))  # Random integers
```

## 🔍 Array Attributes

### Shape and Size

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

print(arr.shape)    # (2, 3) - dimensions
print(arr.size)      # 6 - total elements
print(arr.ndim)      # 2 - number of dimensions
print(arr.dtype)     # int64 - data type
print(arr.itemsize)  # 8 - bytes per element
print(arr.nbytes)    # 48 - total bytes
```

### Data Types

```python
# Specify data type
arr_int = np.array([1, 2, 3], dtype=np.int32)
arr_float = np.array([1.0, 2.0, 3.0], dtype=np.float64)
arr_bool = np.array([True, False, True], dtype=bool)

# Convert data type
arr_float = arr_int.astype(float)
```

## 🎯 Indexing and Slicing

### 1D Array Indexing

```python
arr = np.array([10, 20, 30, 40, 50])

print(arr[0])      # 10 - first element
print(arr[-1])     # 50 - last element
print(arr[1:4])    # [20 30 40] - slice
print(arr[::2])    # [10 30 50] - every other element
```

### 2D Array Indexing

```python
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

print(arr[0, 0])     # 1 - element at row 0, col 0
print(arr[1, :])      # [4 5 6] - entire row 1
print(arr[:, 2])      # [3 6 9] - entire column 2
print(arr[0:2, 1:3])  # [[2 3] [5 6]] - subarray
```

### Boolean Indexing

```python
arr = np.array([1, 2, 3, 4, 5, 6])

# Select elements greater than 3
mask = arr > 3
print(arr[mask])  # [4 5 6]

# Direct boolean indexing
print(arr[arr > 3])  # [4 5 6]

# Multiple conditions
print(arr[(arr > 2) & (arr < 6)])  # [3 4 5]
```

## 🔢 Array Operations

### Arithmetic Operations

```python
arr1 = np.array([1, 2, 3, 4])
arr2 = np.array([5, 6, 7, 8])

# Element-wise operations
print(arr1 + arr2)  # [ 6  8 10 12]
print(arr1 - arr2)  # [-4 -4 -4 -4]
print(arr1 * arr2)  # [ 5 12 21 32]
print(arr1 / arr2)  # [0.2 0.333... 0.428... 0.5]
print(arr1 ** 2)    # [ 1  4  9 16]

# Scalar operations
print(arr1 + 10)    # [11 12 13 14]
print(arr1 * 2)     # [2 4 6 8]
```

### Mathematical Functions

```python
arr = np.array([1, 2, 3, 4, 5])

# Statistical functions
print(np.sum(arr))      # 15
print(np.mean(arr))     # 3.0
print(np.std(arr))      # 1.414...
print(np.min(arr))      # 1
print(np.max(arr))      # 5
print(np.median(arr))   # 3.0

# Mathematical functions
print(np.sin(arr))      # Trigonometric
print(np.exp(arr))      # Exponential
print(np.log(arr))      # Natural logarithm
print(np.sqrt(arr))     # Square root
```

### Array Methods

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

# Aggregation methods
print(arr.sum())        # 21 - sum of all elements
print(arr.sum(axis=0))  # [5 7 9] - sum along rows (columns)
print(arr.sum(axis=1))  # [6 15] - sum along columns (rows)

print(arr.mean())       # 3.5
print(arr.max())        # 6
print(arr.min())        # 1
```

## 🔄 Array Manipulation

### Reshaping

```python
arr = np.arange(12)

# Reshape
reshaped = arr.reshape(3, 4)
print(reshaped.shape)  # (3, 4)

# Flatten
flattened = reshaped.flatten()
print(flattened)  # [0 1 2 ... 11]

# Transpose
transposed = reshaped.T
print(transposed.shape)  # (4, 3)
```

### Concatenation

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

# Concatenate
combined = np.concatenate([arr1, arr2])
print(combined)  # [1 2 3 4 5 6]

# Stack
stacked = np.stack([arr1, arr2])
print(stacked)
# [[1 2 3]
#  [4 5 6]]
```

## 📋 Module 3 Exercises

### Exercise 1: Array Creation
1. Create a 3x3 array of zeros
2. Create a 5x5 array filled with the number 7
3. Create an array with numbers from 0 to 20 (step 2)
4. Create a 2x4 array of random numbers between 0 and 1

### Exercise 2: Indexing Practice
Given the array:
```python
arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
```
1. Extract the second row
2. Extract the third column
3. Extract the 2x2 subarray from the top-left
4. Find all elements greater than 5

### Exercise 3: Operations
1. Create two arrays and perform all arithmetic operations
2. Calculate mean, std, min, max of an array
3. Reshape a 1D array of 12 elements into a 3x4 array

## 🔗 Additional Resources

- [NumPy Array Creation](https://numpy.org/doc/stable/user/basics.creation.html)
- [NumPy Indexing](https://numpy.org/doc/stable/user/basics.indexing.html)
- [NumPy Array Operations](https://numpy.org/doc/stable/user/basics.types.html)

## ✅ Module 3 Checklist

Before moving to advanced topics, ensure you can:

- [ ] Create arrays using various methods
- [ ] Understand and use array attributes
- [ ] Perform indexing and slicing operations
- [ ] Use boolean indexing
- [ ] Perform array operations and use mathematical functions
- [ ] Reshape and manipulate arrays

---

**Next Steps**: Continue with advanced NumPy topics or move to practical applications

