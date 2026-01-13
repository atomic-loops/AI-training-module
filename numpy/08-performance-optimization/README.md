# Module 8: Performance Optimization

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Understand NumPy's performance characteristics
- Use vectorization instead of loops
- Optimize memory usage
- Profile and benchmark NumPy code
- Apply best practices for performance

## ⚡ Vectorization vs Loops

### The Performance Difference

```python
import numpy as np
import time

# Slow: Python loop
def slow_sum(arr):
    result = 0
    for x in arr:
        result += x
    return result

# Fast: NumPy vectorization
def fast_sum(arr):
    return np.sum(arr)

# Benchmark
arr = np.arange(1000000)

start = time.time()
slow_sum(arr)
slow_time = time.time() - start

start = time.time()
fast_sum(arr)
fast_time = time.time() - start

print(f"Loop: {slow_time:.4f}s, Vectorized: {fast_time:.4f}s")
# Vectorized is typically 50-100x faster!
```

### Vectorization Examples

```python
# ❌ Slow: Loop
result = []
for x in arr:
    result.append(x * 2)

# ✅ Fast: Vectorized
result = arr * 2

# ❌ Slow: Conditional loop
result = []
for x in arr:
    if x > 5:
        result.append(x * 2)
    else:
        result.append(x)

# ✅ Fast: Vectorized
result = np.where(arr > 5, arr * 2, arr)
```

## 🎯 Broadcasting for Performance

```python
# ❌ Slow: Loop
arr = np.random.rand(1000, 1000)
row = np.random.rand(1000)
result = np.zeros_like(arr)
for i in range(arr.shape[0]):
    result[i] = arr[i] + row

# ✅ Fast: Broadcasting
result = arr + row  # Automatically broadcasts
```

## 💾 Memory Optimization

### Data Type Selection

```python
# Default: float64 (8 bytes per element)
arr_default = np.array([1.0, 2.0, 3.0])
print(arr_default.dtype)  # float64
print(arr_default.nbytes)  # 24 bytes

# Optimized: float32 (4 bytes per element)
arr_optimized = np.array([1.0, 2.0, 3.0], dtype=np.float32)
print(arr_optimized.dtype)  # float32
print(arr_optimized.nbytes)  # 12 bytes (50% reduction!)

# For integers
arr_int32 = np.array([1, 2, 3], dtype=np.int32)  # 4 bytes
arr_int64 = np.array([1, 2, 3], dtype=np.int64)  # 8 bytes
```

### Memory-Efficient Operations

```python
# ❌ Creates new array
arr = arr * 2

# ✅ Modifies in place (saves memory)
arr *= 2

# ❌ Creates copy
result = arr.copy()

# ✅ Use view when possible
result = arr[:]  # View, not copy
```

### Contiguous Arrays

```python
# Check if array is contiguous
arr = np.arange(12).reshape(3, 4)
print(arr.flags['C_CONTIGUOUS'])  # True

# Non-contiguous (view)
arr_slice = arr[::2, ::2]
print(arr_slice.flags['C_CONTIGUOUS'])  # False

# Make contiguous if needed
arr_contiguous = np.ascontiguousarray(arr_slice)
```

## 🔍 Profiling NumPy Code

### Using timeit

```python
import timeit

# Time a single operation
time = timeit.timeit('np.sum(arr)', 
                     setup='import numpy as np; arr = np.arange(1000000)',
                     number=100)
print(f"Average time: {time/100:.6f}s")
```

### Using cProfile

```python
import cProfile

def my_function():
    arr = np.random.rand(1000, 1000)
    result = np.sum(arr, axis=1)
    return result

cProfile.run('my_function()')
```

### Manual Timing

```python
import time

start = time.perf_counter()  # More precise than time.time()
# ... your code ...
elapsed = time.perf_counter() - start
print(f"Time: {elapsed:.6f}s")
```

## 🚀 Optimization Techniques

### Pre-allocate Arrays

```python
# ❌ Slow: Growing array
result = np.array([])
for i in range(1000):
    result = np.append(result, i)

# ✅ Fast: Pre-allocate
result = np.zeros(1000)
for i in range(1000):
    result[i] = i

# ✅✅ Fastest: Vectorized
result = np.arange(1000)
```

### Use Appropriate Functions

```python
# For large arrays, use optimized functions
arr = np.random.rand(1000000)

# ✅ Fast: NumPy's optimized sum
result = np.sum(arr)

# ❌ Slower: Python's built-in sum
result = sum(arr)  # Converts to Python list first!
```

### Avoid Unnecessary Copies

```python
# ❌ Creates copy
arr2 = arr.copy()

# ✅ Use view when possible
arr2 = arr[:]

# Check if copy is needed
arr2 = arr.view()  # Explicit view
```

## 📊 NumPy's Optimized Routines

### Using BLAS/LAPACK

NumPy uses optimized libraries automatically:

```python
# Matrix multiplication uses optimized BLAS
A = np.random.rand(1000, 1000)
B = np.random.rand(1000, 1000)
C = A @ B  # Automatically uses optimized routines
```

### Compiled Extensions

For extreme performance, consider:
- **Numba**: JIT compilation for NumPy code
- **Cython**: Compile Python to C
- **NumExpr**: Fast numerical array expression evaluator

```python
# Example with Numba
from numba import jit

@jit(nopython=True)
def fast_function(arr):
    return np.sum(arr ** 2)
```

## 🎯 Best Practices Summary

1. **Always vectorize**: Avoid Python loops
2. **Use appropriate dtypes**: Don't use float64 when float32 suffices
3. **Pre-allocate arrays**: Don't grow arrays dynamically
4. **Use in-place operations**: When possible (`+=`, `*=`, etc.)
5. **Profile first**: Measure before optimizing
6. **Use views**: Avoid unnecessary copies
7. **Leverage broadcasting**: Let NumPy handle shape differences

## 📋 Module 8 Exercises

### Exercise 1: Vectorization
1. Rewrite a loop-based function using vectorization
2. Compare performance between loop and vectorized versions
3. Use `np.where` for conditional operations

### Exercise 2: Memory Optimization
1. Compare memory usage of different dtypes
2. Use in-place operations to reduce memory
3. Identify and eliminate unnecessary copies

### Exercise 3: Profiling
1. Profile a NumPy function using timeit
2. Identify bottlenecks in your code
3. Optimize the slowest parts

## 🔗 Additional Resources

- [NumPy Performance Tips](https://numpy.org/doc/stable/user/basics.performance.html)
- [NumPy Memory Layout](https://numpy.org/doc/stable/reference/arrays.ndarray.html#memory-layout)
- [Numba Documentation](https://numba.pydata.org/)

## ✅ Module 8 Checklist

Before moving to Module 9, ensure you can:

- [ ] Understand the performance difference between loops and vectorization
- [ ] Optimize memory usage with appropriate dtypes
- [ ] Profile NumPy code to identify bottlenecks
- [ ] Apply optimization techniques effectively
- [ ] Use in-place operations and views appropriately

---

**Next Module**: [Module 9: Best Practices](../09-best-practices/README.md)

