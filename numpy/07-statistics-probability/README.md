# Module 7: Statistics & Probability

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Calculate descriptive statistics
- Generate random numbers and samples
- Work with probability distributions
- Perform statistical tests
- Use NumPy's random module effectively

## 📊 Descriptive Statistics

### Central Tendency

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Mean
mean = np.mean(arr)  # 5.5

# Median
median = np.median(arr)  # 5.5

# Mode (requires scipy)
from scipy import stats
mode = stats.mode(arr)  # Most frequent value

# Weighted mean
weights = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
weighted_mean = np.average(arr, weights=weights)
```

### Dispersion

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Standard deviation
std = np.std(arr)  # Population std
std_sample = np.std(arr, ddof=1)  # Sample std

# Variance
var = np.var(arr)  # Population variance
var_sample = np.var(arr, ddof=1)  # Sample variance

# Range
range_val = np.ptp(arr)  # Peak-to-peak (max - min)

# Percentiles
p25 = np.percentile(arr, 25)  # 25th percentile
p50 = np.percentile(arr, 50)  # Median
p75 = np.percentile(arr, 75)  # 75th percentile

# Interquartile range
iqr = np.percentile(arr, 75) - np.percentile(arr, 25)
```

### Summary Statistics

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# All at once
print(f"Min: {np.min(arr)}")
print(f"Max: {np.max(arr)}")
print(f"Mean: {np.mean(arr)}")
print(f"Std: {np.std(arr)}")
print(f"Sum: {np.sum(arr)}")
```

## 🎲 Random Number Generation

### Basic Random Numbers

```python
# Set seed for reproducibility
np.random.seed(42)

# Random float in [0, 1)
random_float = np.random.random()

# Random array
random_array = np.random.random((3, 3))

# Random integers
random_int = np.random.randint(0, 10)  # Single integer
random_ints = np.random.randint(0, 10, size=(3, 3))  # Array
```

### Random Sampling

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Random choice
choice = np.random.choice(arr)  # Single random element
choices = np.random.choice(arr, size=5)  # 5 random elements
choices_weighted = np.random.choice(arr, size=5, p=[0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1])

# Random permutation
permuted = np.random.permutation(arr)  # Shuffled copy
np.random.shuffle(arr)  # Shuffle in place
```

## 📈 Probability Distributions

### Uniform Distribution

```python
# Uniform [0, 1)
uniform = np.random.uniform(0, 1, size=1000)

# Uniform [a, b)
uniform_range = np.random.uniform(5, 10, size=1000)
```

### Normal (Gaussian) Distribution

```python
# Standard normal (mean=0, std=1)
normal = np.random.normal(0, 1, size=1000)

# Custom normal (mean=mu, std=sigma)
normal_custom = np.random.normal(50, 10, size=1000)

# Using random.normal
from numpy.random import normal
samples = normal(loc=0, scale=1, size=1000)
```

### Other Distributions

```python
# Binomial
binomial = np.random.binomial(n=10, p=0.5, size=1000)

# Poisson
poisson = np.random.poisson(lam=5, size=1000)

# Exponential
exponential = np.random.exponential(scale=1.0, size=1000)

# Beta
beta = np.random.beta(a=2, b=5, size=1000)

# Gamma
gamma = np.random.gamma(shape=2, scale=2, size=1000)
```

## 📊 Statistical Functions

### Correlation and Covariance

```python
x = np.array([1, 2, 3, 4, 5])
y = np.array([2, 4, 6, 8, 10])

# Correlation coefficient
correlation = np.corrcoef(x, y)[0, 1]

# Covariance matrix
covariance = np.cov(x, y)

# Cross-correlation
cross_corr = np.correlate(x, y, mode='full')
```

### Histogram

```python
data = np.random.normal(0, 1, 1000)

# Histogram
counts, bins = np.histogram(data, bins=10)

# Histogram with density
counts, bins = np.histogram(data, bins=10, density=True)
```

### Cumulative Statistics

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Cumulative sum
cumsum = np.cumsum(arr)  # [1 3 6 10 15 21 28 36 45 55]

# Cumulative product
cumprod = np.cumprod(arr)

# Cumulative maximum
cummax = np.maximum.accumulate(arr)
```

## 🎯 Array Statistics Along Axes

```python
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# Mean along axis 0 (columns)
mean_cols = np.mean(arr, axis=0)  # [4. 5. 6.]

# Mean along axis 1 (rows)
mean_rows = np.mean(arr, axis=1)  # [2. 5. 8.]

# Standard deviation along axis
std_cols = np.std(arr, axis=0)
std_rows = np.std(arr, axis=1)
```

## 🔢 Quantiles and Percentiles

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Quantiles
q1 = np.quantile(arr, 0.25)  # First quartile
q2 = np.quantile(arr, 0.50)  # Median
q3 = np.quantile(arr, 0.75)  # Third quartile

# Multiple quantiles at once
quantiles = np.quantile(arr, [0.25, 0.5, 0.75])

# Percentiles (same as quantiles * 100)
p50 = np.percentile(arr, 50)  # Same as median
```

## 📋 Module 7 Exercises

### Exercise 1: Descriptive Statistics
1. Generate a dataset and calculate mean, median, std, variance
2. Calculate percentiles and IQR
3. Create a summary statistics report

### Exercise 2: Random Sampling
1. Generate random samples from different distributions
2. Create a weighted random choice function
3. Shuffle and sample from an array

### Exercise 3: Statistical Analysis
1. Calculate correlation between two datasets
2. Create histograms for different distributions
3. Calculate cumulative statistics

## 🔗 Additional Resources

- [NumPy Random Sampling](https://numpy.org/doc/stable/reference/random/index.html)
- [NumPy Statistical Functions](https://numpy.org/doc/stable/reference/routines.statistics.html)
- [Probability Distributions](https://numpy.org/doc/stable/reference/random/generator.html#distributions)

## ✅ Module 7 Checklist

Before moving to Module 8, ensure you can:

- [ ] Calculate descriptive statistics (mean, median, std, variance)
- [ ] Generate random numbers and samples
- [ ] Work with probability distributions
- [ ] Calculate correlations and covariances
- [ ] Use quantiles and percentiles
- [ ] Compute statistics along different axes

---

**Next Module**: [Module 8: Performance Optimization](../08-performance-optimization/README.md)

