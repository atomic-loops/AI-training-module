# Module 10: Common Pitfalls & Solutions

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Identify common NumPy mistakes
- Understand why these mistakes occur
- Apply correct solutions
- Avoid performance pitfalls
- Debug NumPy issues effectively

## ⚠️ Pitfall 1: Views vs Copies

### The Problem

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
view = arr[1:4]  # This is a VIEW, not a copy!
view[0] = 99
print(arr)  # [1 99 3 4 5] - Original changed!
```

### The Solution

```python
# ✅ Explicit copy when needed
arr = np.array([1, 2, 3, 4, 5])
copy = arr[1:4].copy()  # Explicit copy
copy[0] = 99
print(arr)  # [1 2 3 4 5] - Original unchanged
```

## ⚠️ Pitfall 2: Mutating During Iteration

### The Problem

```python
# ❌ Don't modify array while iterating
arr = np.array([1, 2, 3, 4, 5])
for i, val in enumerate(arr):
    if val > 3:
        arr[i] = 0  # Can cause unexpected behavior
```

### The Solution

```python
# ✅ Use boolean indexing
arr = np.array([1, 2, 3, 4, 5])
arr[arr > 3] = 0  # Clean and efficient

# Or create a new array
arr = np.array([1, 2, 3, 4, 5])
new_arr = np.where(arr > 3, 0, arr)
```

## ⚠️ Pitfall 3: Using Python's Built-in Functions

### The Problem

```python
# ❌ Slow: Python's sum
arr = np.arange(1000000)
result = sum(arr)  # Converts to list, very slow!

# ❌ Slow: Python's max/min
result = max(arr)  # Also slow
```

### The Solution

```python
# ✅ Fast: NumPy's methods
arr = np.arange(1000000)
result = np.sum(arr)  # or arr.sum()
result = np.max(arr)  # or arr.max()
result = np.min(arr)  # or arr.min()
```

## ⚠️ Pitfall 4: Incorrect Broadcasting

### The Problem

```python
# ❌ Shape mismatch error
arr1 = np.array([[1, 2, 3], [4, 5, 6]])  # Shape (2, 3)
arr2 = np.array([1, 2])  # Shape (2,)
result = arr1 + arr2  # Error: cannot broadcast
```

### The Solution

```python
# ✅ Reshape for broadcasting
arr1 = np.array([[1, 2, 3], [4, 5, 6]])  # Shape (2, 3)
arr2 = np.array([1, 2])  # Shape (2,)
arr2 = arr2[:, np.newaxis]  # Reshape to (2, 1)
result = arr1 + arr2  # Now it works!

# Or use np.newaxis
result = arr1 + arr2[:, np.newaxis]
```

## ⚠️ Pitfall 5: NaN and Infinity Issues

### The Problem

```python
# ❌ NaN propagation
arr = np.array([1, 2, np.nan, 4, 5])
result = np.sum(arr)  # Returns nan!
mean = np.mean(arr)  # Returns nan!
```

### The Solution

```python
# ✅ Handle NaN explicitly
arr = np.array([1, 2, np.nan, 4, 5])
result = np.nansum(arr)  # Ignores NaN
mean = np.nanmean(arr)  # Ignores NaN

# Or filter NaN first
clean_arr = arr[~np.isnan(arr)]
result = np.sum(clean_arr)
```

## ⚠️ Pitfall 6: Integer Division

### The Problem

```python
# ❌ Integer division (Python 2 style)
arr = np.array([1, 2, 3, 4, 5], dtype=int)
result = arr / 2  # Returns float array [0.5, 1.0, 1.5, ...]
```

### The Solution

```python
# ✅ Use floor division for integers
arr = np.array([1, 2, 3, 4, 5], dtype=int)
result = arr // 2  # Integer division [0, 1, 1, 2, 2]

# Or use np.floor_divide
result = np.floor_divide(arr, 2)
```

## ⚠️ Pitfall 7: Memory Issues with Large Arrays

### The Problem

```python
# ❌ Creating unnecessary copies
large_arr = np.random.rand(10000, 10000)
copy1 = large_arr.copy()  # 800MB copy!
copy2 = large_arr.copy()  # Another 800MB!
# Now using 2.4GB instead of 800MB
```

### The Solution

```python
# ✅ Use views when possible
large_arr = np.random.rand(10000, 10000)
view1 = large_arr[:]  # View, not copy
view2 = large_arr[::2]  # View with stride

# Only copy when necessary
copy = large_arr.copy()  # Only when you need independent data
```

## ⚠️ Pitfall 8: Wrong Data Types

### The Problem

```python
# ❌ Using float64 when float32 would suffice
arr = np.array([1.0, 2.0, 3.0])  # Defaults to float64 (8 bytes)
# Uses 2x more memory than needed
```

### The Solution

```python
# ✅ Use appropriate dtype
arr = np.array([1.0, 2.0, 3.0], dtype=np.float32)  # 4 bytes
# Saves 50% memory for large arrays
```

## ⚠️ Pitfall 9: Comparing Floating Point Numbers

### The Problem

```python
# ❌ Floating point precision issues
arr = np.array([0.1, 0.2, 0.3])
result = np.sum(arr)
print(result == 0.6)  # False! (due to floating point precision)
```

### The Solution

```python
# ✅ Use np.isclose or np.allclose
arr = np.array([0.1, 0.2, 0.3])
result = np.sum(arr)
print(np.isclose(result, 0.6))  # True
print(np.allclose(result, 0.6))  # True

# For arrays
arr1 = np.array([0.1, 0.2, 0.3])
arr2 = np.array([0.1, 0.2, 0.3])
print(np.allclose(arr1, arr2))  # True
```

## ⚠️ Pitfall 10: Modifying Arrays in Functions

### The Problem

```python
# ❌ Function modifies input unexpectedly
def process_array(arr):
    arr[0] = 999  # Modifies original!
    return arr

original = np.array([1, 2, 3])
result = process_array(original)
print(original)  # [999 2 3] - Changed!
```

### The Solution

```python
# ✅ Copy inside function if modification needed
def process_array(arr):
    arr = arr.copy()  # Work on copy
    arr[0] = 999
    return arr

# Or document that function modifies input
def process_array_inplace(arr):
    """Modifies arr in place. Use arr.copy() if you need original."""
    arr[0] = 999
    return arr
```

## 🔍 Debugging Tips

### Check Array Properties

```python
arr = np.array([1, 2, 3, 4, 5])

# Debug information
print(f"Shape: {arr.shape}")
print(f"Dtype: {arr.dtype}")
print(f"Size: {arr.size}")
print(f"Memory: {arr.nbytes} bytes")
print(f"Is view: {arr.base is not None}")
print(f"Is contiguous: {arr.flags['C_CONTIGUOUS']}")
```

### Common Error Messages

```python
# ValueError: operands could not be broadcast together
# Solution: Check shapes, use reshape or np.newaxis

# MemoryError
# Solution: Use smaller arrays, optimize dtype, use views

# TypeError: only integer scalar arrays can be converted to a scalar index
# Solution: Use .item() to extract scalar from array
```

## 📋 Module 10 Exercises

### Exercise 1: Identify Pitfalls
1. Review code snippets and identify pitfalls
2. Explain why each is a problem
3. Provide corrected versions

### Exercise 2: Fix Common Errors
1. Fix code with view/copy issues
2. Correct broadcasting errors
3. Handle NaN and floating point issues

### Exercise 3: Debug Practice
1. Write code with intentional pitfalls
2. Debug and fix the issues
3. Verify solutions work correctly

## 🔗 Additional Resources

- [NumPy Troubleshooting](https://numpy.org/doc/stable/user/troubleshooting.html)
- [Common NumPy Errors](https://numpy.org/doc/stable/reference/errors.html)
- [NumPy FAQ](https://numpy.org/doc/stable/user/faq.html)

## ✅ Module 10 Checklist

Before moving to Module 11, ensure you can:

- [ ] Identify common NumPy pitfalls
- [ ] Understand views vs copies
- [ ] Handle NaN and floating point issues
- [ ] Fix broadcasting errors
- [ ] Debug NumPy code effectively
- [ ] Avoid memory and performance pitfalls

---

**Next Module**: [Module 11: Integration with Other Libraries](../11-integration/README.md)

