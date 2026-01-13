# Module 6: Linear Algebra with NumPy

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Perform matrix operations
- Solve linear systems
- Calculate eigenvalues and eigenvectors
- Use matrix decompositions
- Apply linear algebra functions effectively

## 🔢 Matrix Operations

### Matrix Multiplication

```python
import numpy as np

# Create matrices
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# Matrix multiplication
C = np.dot(A, B)
# or using @ operator (Python 3.5+)
C = A @ B

# Element-wise multiplication
C = A * B
```

### Dot Product

```python
# 1D arrays - inner product
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
result = np.dot(a, b)  # 1*4 + 2*5 + 3*6 = 32

# 2D arrays - matrix multiplication
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
result = np.dot(A, B)
```

### Outer Product

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
result = np.outer(a, b)
# [[ 4  5  6]
#  [ 8 10 12]
#  [12 15 18]]
```

## 🔍 Matrix Properties

### Transpose

```python
A = np.array([[1, 2, 3], [4, 5, 6]])
A_T = A.T
# or
A_T = np.transpose(A)
```

### Determinant

```python
A = np.array([[1, 2], [3, 4]])
det = np.linalg.det(A)  # -2.0
```

### Trace

```python
A = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
trace = np.trace(A)  # 15 (sum of diagonal)
```

### Rank

```python
A = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
rank = np.linalg.matrix_rank(A)
```

## 🧮 Solving Linear Systems

### Solving Ax = b

```python
# System: 3x + y = 9, x + 2y = 8
A = np.array([[3, 1], [1, 2]])
b = np.array([9, 8])

# Solve
x = np.linalg.solve(A, b)
# x = [2, 3]
```

### Least Squares Solution

```python
# Overdetermined system
A = np.array([[1, 1], [1, 2], [1, 3]])
b = np.array([1, 2, 2])

# Least squares solution
x = np.linalg.lstsq(A, b, rcond=None)[0]
```

## 🔬 Eigenvalues and Eigenvectors

### Computing Eigenvalues and Eigenvectors

```python
A = np.array([[1, 2], [2, 1]])

# Eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(A)

print("Eigenvalues:", eigenvalues)
print("Eigenvectors:", eigenvectors)
```

### Eigendecomposition

```python
A = np.array([[4, 2], [2, 4]])

# Eigendecomposition: A = Q * Lambda * Q^-1
eigenvalues, eigenvectors = np.linalg.eig(A)

# Reconstruct
Lambda = np.diag(eigenvalues)
A_reconstructed = eigenvectors @ Lambda @ np.linalg.inv(eigenvectors)
```

## 📐 Matrix Decompositions

### LU Decomposition

```python
from scipy.linalg import lu

A = np.array([[2, 1, 0], [1, 2, 1], [0, 1, 2]])
P, L, U = lu(A)

# P: Permutation matrix
# L: Lower triangular
# U: Upper triangular
# A = P @ L @ U
```

### QR Decomposition

```python
A = np.array([[1, 2], [3, 4], [5, 6]])

Q, R = np.linalg.qr(A)

# Q: Orthogonal matrix
# R: Upper triangular
# A = Q @ R
```

### SVD (Singular Value Decomposition)

```python
A = np.array([[1, 2, 3], [4, 5, 6]])

U, s, Vt = np.linalg.svd(A)

# U: Left singular vectors
# s: Singular values
# Vt: Right singular vectors (transposed)
# A = U @ diag(s) @ Vt
```

## 🎯 Special Matrices

### Identity Matrix

```python
I = np.eye(3)  # 3x3 identity matrix
```

### Diagonal Matrix

```python
# Create from diagonal
diag = np.diag([1, 2, 3])

# Extract diagonal
A = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
diagonal = np.diag(A)  # [1 5 9]
```

### Inverse Matrix

```python
A = np.array([[1, 2], [3, 4]])
A_inv = np.linalg.inv(A)

# Verify
I = A @ A_inv  # Should be identity matrix
```

### Pseudo-inverse

```python
A = np.array([[1, 2], [3, 4], [5, 6]])
A_pinv = np.linalg.pinv(A)  # Moore-Penrose pseudo-inverse
```

## 📊 Matrix Norms

```python
A = np.array([[1, 2], [3, 4]])

# Frobenius norm
frobenius = np.linalg.norm(A, 'fro')

# Matrix norm (default is Frobenius)
norm = np.linalg.norm(A)

# Other norms
norm_1 = np.linalg.norm(A, 1)  # L1 norm
norm_2 = np.linalg.norm(A, 2)  # L2 norm
norm_inf = np.linalg.norm(A, np.inf)  # Infinity norm
```

## 🔄 Vector Operations

### Cross Product

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
cross = np.cross(a, b)  # [-3 6 -3]
```

### Vector Norms

```python
v = np.array([3, 4])

# L2 norm (Euclidean)
norm = np.linalg.norm(v)  # 5.0

# L1 norm
norm_1 = np.linalg.norm(v, 1)  # 7.0
```

## 📋 Module 6 Exercises

### Exercise 1: Matrix Operations
1. Create two matrices and perform matrix multiplication
2. Calculate the determinant and trace of a matrix
3. Find the inverse of a matrix and verify it

### Exercise 2: Linear Systems
1. Solve a system of linear equations
2. Find the least squares solution for an overdetermined system
3. Check if a system has a unique solution

### Exercise 3: Decompositions
1. Perform eigendecomposition on a matrix
2. Perform SVD on a matrix
3. Reconstruct the original matrix from its decomposition

## 🔗 Additional Resources

- [NumPy Linear Algebra](https://numpy.org/doc/stable/reference/routines.linalg.html)
- [Linear Algebra with NumPy](https://www.geeksforgeeks.org/numpy/numpy-linear-algebra/)
- [Matrix Operations Guide](https://numpy.org/doc/stable/reference/generated/numpy.linalg.solve.html)

## ✅ Module 6 Checklist

Before moving to Module 7, ensure you can:

- [ ] Perform matrix multiplication and dot products
- [ ] Calculate matrix properties (determinant, trace, rank)
- [ ] Solve linear systems
- [ ] Compute eigenvalues and eigenvectors
- [ ] Use matrix decompositions (LU, QR, SVD)
- [ ] Work with matrix inverses and norms

---

**Next Module**: [Module 7: Statistics & Probability](../07-statistics-probability/README.md)

