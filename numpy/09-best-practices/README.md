# Module 9: NumPy Best Practices

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Follow NumPy coding conventions
- Write clean and readable NumPy code
- Avoid common anti-patterns
- Use NumPy idioms effectively
- Write maintainable NumPy code

## 📝 Code Style and Conventions

### Import Convention

```python
# ✅ Standard and expected
import numpy as np

# ❌ Non-standard
import numpy
import numpy as num
from numpy import *
```

### Naming Conventions

```python
# ✅ Good: Descriptive names
data_array = np.array([1, 2, 3])
matrix_a = np.array([[1, 2], [3, 4]])
temperature_data = np.random.normal(20, 5, 100)

# ❌ Bad: Unclear names
arr = np.array([1, 2, 3])
a = np.array([[1, 2], [3, 4]])
x = np.random.normal(20, 5, 100)
```

### Array Creation

```python
# ✅ Explicit and clear
arr = np.array([1, 2, 3, 4, 5])

# ✅ Use appropriate constructors
zeros = np.zeros((3, 4))
ones = np.ones((2, 3))
range_arr = np.arange(0, 10, 2)

# ❌ Unclear
arr = np.array(range(5))  # Less efficient than np.arange
```

## 🎯 NumPy Idioms

### Use Vectorized Operations

```python
# ✅ Idiomatic: Vectorized
arr = np.array([1, 2, 3, 4, 5])
squared = arr ** 2
sum_result = arr.sum()

# ❌ Anti-pattern: Loop
squared = []
for x in arr:
    squared.append(x ** 2)
```

### Boolean Indexing

```python
# ✅ Idiomatic: Boolean indexing
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
filtered = arr[arr > 5]

# ❌ Anti-pattern: Loop with condition
filtered = []
for x in arr:
    if x > 5:
        filtered.append(x)
```

### Broadcasting

```python
# ✅ Idiomatic: Let NumPy broadcast
arr = np.array([[1, 2, 3], [4, 5, 6]])
row = np.array([10, 20, 30])
result = arr + row  # Broadcasting

# ❌ Anti-pattern: Manual broadcasting
result = np.zeros_like(arr)
for i in range(arr.shape[0]):
    result[i] = arr[i] + row
```

## 🔧 Error Handling

### Validate Inputs

```python
def process_array(arr):
    # ✅ Validate input
    if not isinstance(arr, np.ndarray):
        raise TypeError("Input must be a NumPy array")
    
    if arr.size == 0:
        raise ValueError("Array cannot be empty")
    
    # Process array
    return arr * 2
```

### Handle Edge Cases

```python
def safe_divide(a, b):
    # ✅ Handle division by zero
    with np.errstate(divide='ignore', invalid='ignore'):
        result = np.divide(a, b)
        result = np.where(np.isfinite(result), result, 0)
    return result
```

## 📊 Documentation

### Docstrings

```python
def calculate_statistics(data):
    """
    Calculate descriptive statistics for an array.
    
    Parameters
    ----------
    data : np.ndarray
        Input array of numerical data
        
    Returns
    -------
    dict
        Dictionary containing mean, std, min, max
        
    Examples
    --------
    >>> data = np.array([1, 2, 3, 4, 5])
    >>> stats = calculate_statistics(data)
    >>> stats['mean']
    3.0
    """
    return {
        'mean': np.mean(data),
        'std': np.std(data),
        'min': np.min(data),
        'max': np.max(data)
    }
```

## 🎨 Code Organization

### Separate Concerns

```python
# ✅ Good: Separate data preparation and computation
def prepare_data(raw_data):
    """Clean and prepare data."""
    data = np.array(raw_data)
    data = data[~np.isnan(data)]  # Remove NaN
    return data

def compute_statistics(data):
    """Compute statistics on clean data."""
    return {
        'mean': np.mean(data),
        'std': np.std(data)
    }

# Usage
clean_data = prepare_data(raw_data)
stats = compute_statistics(clean_data)
```

### Use Functions

```python
# ✅ Good: Reusable function
def normalize_array(arr):
    """Normalize array to [0, 1] range."""
    arr_min = arr.min()
    arr_max = arr.max()
    return (arr - arr_min) / (arr_max - arr_min)

# ❌ Bad: Repeated code
arr1_normalized = (arr1 - arr1.min()) / (arr1.max() - arr1.min())
arr2_normalized = (arr2 - arr2.min()) / (arr2.max() - arr2.min())
```

## 🚫 Common Anti-patterns

### Don't Mix NumPy and Python Lists Unnecessarily

```python
# ❌ Bad: Converting back and forth
python_list = [1, 2, 3, 4, 5]
arr = np.array(python_list)
result_list = arr.tolist()
arr2 = np.array(result_list)

# ✅ Good: Stay in NumPy
arr = np.array([1, 2, 3, 4, 5])
result = arr * 2  # Keep as NumPy array
```

### Don't Use Python's sum() on Arrays

```python
# ❌ Slow: Python's sum
arr = np.arange(1000000)
result = sum(arr)  # Converts to list first!

# ✅ Fast: NumPy's sum
result = np.sum(arr)  # or arr.sum()
```

### Avoid Unnecessary Copies

```python
# ❌ Unnecessary copy
arr2 = arr.copy()  # Only if you need to modify independently

# ✅ Use view when possible
arr2 = arr[:]  # View, not copy
```

## ✅ Type Hints (Python 3.5+)

```python
from typing import Union
import numpy as np

def process_array(arr: np.ndarray) -> np.ndarray:
    """Process array and return result."""
    return arr * 2

def combine_arrays(a: np.ndarray, b: np.ndarray) -> np.ndarray:
    """Combine two arrays."""
    return np.concatenate([a, b])
```

## 🧪 Testing

### Unit Tests

```python
import unittest
import numpy as np

class TestArrayOperations(unittest.TestCase):
    def test_array_sum(self):
        arr = np.array([1, 2, 3])
        self.assertEqual(arr.sum(), 6)
    
    def test_array_mean(self):
        arr = np.array([1, 2, 3, 4, 5])
        self.assertAlmostEqual(arr.mean(), 3.0)
    
    def test_array_shape(self):
        arr = np.array([[1, 2], [3, 4]])
        self.assertEqual(arr.shape, (2, 2))
```

## 📋 Module 9 Exercises

### Exercise 1: Code Review
1. Review NumPy code and identify anti-patterns
2. Refactor code to follow best practices
3. Add proper documentation

### Exercise 2: Write Clean Code
1. Write a function following NumPy best practices
2. Add type hints and docstrings
3. Include error handling

### Exercise 3: Testing
1. Write unit tests for NumPy functions
2. Test edge cases and error conditions
3. Verify vectorized operations

## 🔗 Additional Resources

- [NumPy Style Guide](https://numpy.org/doc/stable/dev/development_environment.html)
- [PEP 8 Style Guide](https://pep8.org/)
- [NumPy Documentation Standards](https://numpy.org/doc/stable/docs/howto_document.html)

## ✅ Module 9 Checklist

Before moving to Module 10, ensure you can:

- [ ] Follow NumPy coding conventions
- [ ] Write idiomatic NumPy code
- [ ] Avoid common anti-patterns
- [ ] Document code properly
- [ ] Write testable NumPy code
- [ ] Handle errors appropriately

---

**Next Module**: [Module 10: Common Pitfalls](../10-pitfalls/README.md)

