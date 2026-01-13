# Module 4: Advanced Array Operations

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Perform advanced array operations and transformations
- Use broadcasting effectively
- Apply universal functions (ufuncs)
- Work with array stacking and splitting
- Understand array copying vs viewing

## 🔄 Broadcasting

Broadcasting allows NumPy to perform operations on arrays of different shapes.

### Broadcasting Rules

1. Arrays are aligned from the trailing dimension
2. Dimensions must be equal or one of them must be 1
3. Missing dimensions are treated as size 1

### Examples

```python
import numpy as np

# Scalar broadcasting
arr = np.array([[1, 2, 3], [4, 5, 6]])
result = arr + 10  # Adds 10 to every element

# 1D array broadcasting
arr = np.array([[1, 2, 3], [4, 5, 6]])
row = np.array([10, 20, 30])
result = arr + row  # Broadcasts row to each row of arr

# Column broadcasting
arr = np.array([[1, 2, 3], [4, 5, 6]])
col = np.array([[10], [20]])
result = arr + col  # Broadcasts column to each column of arr
```

## 🔧 Universal Functions (ufuncs)

Universal functions operate element-wise on arrays.

### Mathematical ufuncs

```python
arr = np.array([0, np.pi/2, np.pi])

# Trigonometric
np.sin(arr)
np.cos(arr)
np.tan(arr)

# Exponential and logarithmic
np.exp(arr)
np.log(arr)
np.log10(arr)
np.sqrt(arr)

# Power functions
np.power(arr, 2)
arr ** 2
```

### Comparison ufuncs

```python
arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.array([3, 2, 1, 4, 5])

np.equal(arr1, arr2)    # ==
np.not_equal(arr1, arr2)  # !=
np.greater(arr1, arr2)   # >
np.less(arr1, arr2)      # <
np.greater_equal(arr1, arr2)  # >=
np.less_equal(arr1, arr2)     # <=
```

### Logical ufuncs

```python
arr = np.array([True, False, True, False])

np.logical_and(arr, [True, True, False, False])
np.logical_or(arr, [True, False, True, False])
np.logical_not(arr)
np.logical_xor(arr, [True, False, False, True])
```

## 📦 Array Stacking and Splitting

### Stacking Arrays

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

# Vertical stacking
np.vstack([arr1, arr2])
# [[1 2 3]
#  [4 5 6]]

# Horizontal stacking
np.hstack([arr1, arr2])
# [1 2 3 4 5 6]

# Column stacking
np.column_stack([arr1, arr2])
# [[1 4]
#  [2 5]
#  [3 6]]

# Depth stacking
np.dstack([arr1, arr2])
```

### Splitting Arrays

```python
arr = np.array([1, 2, 3, 4, 5, 6])

# Split into equal parts
np.split(arr, 3)  # Splits into 3 equal arrays

# Split at specific indices
np.split(arr, [2, 4])  # Splits at indices 2 and 4

# Horizontal split
arr2d = np.array([[1, 2, 3], [4, 5, 6]])
np.hsplit(arr2d, 3)  # Split horizontally

# Vertical split
np.vsplit(arr2d, 2)  # Split vertically
```

## 🔍 Array Views vs Copies

### Views (No Copy)

```python
arr = np.array([1, 2, 3, 4, 5])
view = arr[1:4]  # Creates a view, not a copy
view[0] = 99
print(arr)  # [1 99 3 4 5] - original is modified!
```

### Copies

```python
arr = np.array([1, 2, 3, 4, 5])
copy = arr[1:4].copy()  # Creates a copy
copy[0] = 99
print(arr)  # [1 2 3 4 5] - original unchanged
```

### When Copies are Made

```python
# These create copies:
arr.copy()
arr.reshape().copy()
np.array(arr)

# These create views:
arr[1:4]
arr.T
arr.reshape()
```

## 🎨 Array Manipulation

### Transpose and Swap Axes

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

# Transpose
arr.T
np.transpose(arr)

# Swap axes
arr.swapaxes(0, 1)
np.swapaxes(arr, 0, 1)
```

### Flatten and Ravel

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

# Flatten (always returns copy)
arr.flatten()

# Ravel (returns view when possible)
arr.ravel()
```

### Reshape Operations

```python
arr = np.arange(12)

# Reshape
arr.reshape(3, 4)
arr.reshape(-1, 4)  # -1 means "infer this dimension"

# Resize (modifies in place)
arr.resize(3, 4)
```

## 📋 Module 4 Exercises

### Exercise 1: Broadcasting
1. Create a 3x4 array and add a 1D array of 4 elements to each row
2. Multiply a 2D array by a scalar
3. Add a column vector to each column of a 2D array

### Exercise 2: Universal Functions
1. Apply trigonometric functions to an array
2. Use comparison functions to filter an array
3. Combine logical operations to create complex conditions

### Exercise 3: Array Manipulation
1. Stack multiple arrays in different ways
2. Split an array into multiple parts
3. Create views and copies, demonstrate the difference

## 🔗 Additional Resources

- [NumPy Broadcasting](https://numpy.org/doc/stable/user/basics.broadcasting.html)
- [NumPy Universal Functions](https://numpy.org/doc/stable/reference/ufuncs.html)
- [NumPy Array Manipulation](https://numpy.org/doc/stable/reference/routines.array-manipulation.html)

## ✅ Module 4 Checklist

Before moving to Module 5, ensure you can:

- [ ] Understand and use broadcasting rules
- [ ] Apply universal functions effectively
- [ ] Stack and split arrays appropriately
- [ ] Distinguish between views and copies
- [ ] Manipulate array shapes and dimensions

---

**Next Module**: [Module 5: Advanced Indexing](../05-indexing-advanced/README.md)

