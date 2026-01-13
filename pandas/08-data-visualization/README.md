# Module 8: Data Visualization with Pandas

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Create basic plots with Pandas
- Customize plot appearance
- Create different chart types
- Combine Pandas with Matplotlib/Seaborn
- Create publication-quality visualizations

## 📊 Basic Plotting

### Simple Line Plot

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Create sample data
df = pd.DataFrame({
    'value': np.random.randn(100).cumsum()
}, index=pd.date_range('2023-01-01', periods=100, freq='D'))

# Basic line plot
df.plot()
plt.show()

# Plot specific column
df['value'].plot()
plt.show()
```

### Customizing Plots

```python
# Customize appearance
df.plot(
    title='Time Series Data',
    xlabel='Date',
    ylabel='Value',
    figsize=(10, 6),
    color='blue',
    linewidth=2
)
plt.show()
```

## 📈 Chart Types

### Line Plot

```python
# Single line
df['value'].plot(kind='line')

# Multiple lines
df.plot(y=['value1', 'value2'])
```

### Bar Plot

```python
# Vertical bars
df.plot(kind='bar')

# Horizontal bars
df.plot(kind='barh')

# Stacked bars
df.plot(kind='bar', stacked=True)

# Grouped bars
df.plot(kind='bar', x='category')
```

### Histogram

```python
# Histogram
df['value'].plot(kind='hist', bins=30)

# Density plot
df['value'].plot(kind='density')

# Both
df['value'].hist(bins=30, density=True, alpha=0.7)
df['value'].plot(kind='density', ax=plt.gca())
```

### Box Plot

```python
# Single box plot
df['value'].plot(kind='box')

# Multiple box plots
df.plot(kind='box')

# Grouped box plots
df.boxplot(column='value', by='category')
```

### Scatter Plot

```python
# Scatter plot
df.plot(kind='scatter', x='x', y='y')

# With size
df.plot(kind='scatter', x='x', y='y', s=df['size'])

# With color
df.plot(kind='scatter', x='x', y='y', c='category', colormap='viridis')
```

### Area Plot

```python
# Area plot
df.plot(kind='area')

# Stacked area
df.plot(kind='area', stacked=True)
```

## 🎨 Advanced Plotting

### Subplots

```python
# Create subplots
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

df['value1'].plot(ax=axes[0, 0], title='Value 1')
df['value2'].plot(ax=axes[0, 1], title='Value 2')
df['value3'].plot(ax=axes[1, 0], title='Value 3')
df['value4'].plot(ax=axes[1, 1], title='Value 4')

plt.tight_layout()
plt.show()
```

### Multiple Y-Axes

```python
# Plot with secondary y-axis
ax = df['value1'].plot(color='blue')
ax2 = ax.twinx()
df['value2'].plot(ax=ax2, color='red')
plt.show()
```

## 📊 Statistical Plots

### Correlation Matrix

```python
# Correlation heatmap
correlation = df.corr()
correlation.plot(kind='heatmap')  # Requires matplotlib/seaborn

# Or use seaborn
import seaborn as sns
sns.heatmap(correlation, annot=True)
plt.show()
```

### Pair Plot

```python
# Pair plot (requires seaborn)
sns.pairplot(df)
plt.show()
```

## 🎯 Time Series Visualization

### Time Series Plots

```python
# Time series with datetime index
df.plot(x='date', y='value')

# Multiple time series
df.plot(y=['value1', 'value2', 'value3'])

# With moving averages
df['ma'] = df['value'].rolling(7).mean()
df[['value', 'ma']].plot()
```

### Seasonal Decomposition

```python
from statsmodels.tsa.seasonal import seasonal_decompose

# Decompose time series
result = seasonal_decompose(df['value'], model='additive', period=30)
result.plot()
plt.show()
```

## 🎨 Styling and Themes

### Using Styles

```python
# Available styles
plt.style.available

# Apply style
plt.style.use('seaborn-v0_8')
df.plot()

# Or use seaborn style
sns.set_style('whitegrid')
df.plot()
```

### Custom Styling

```python
# Customize plot
ax = df.plot(
    figsize=(12, 6),
    color='steelblue',
    linewidth=2,
    linestyle='--',
    marker='o',
    markersize=4
)

# Customize axes
ax.set_title('Custom Plot', fontsize=16, fontweight='bold')
ax.set_xlabel('X Label', fontsize=12)
ax.set_ylabel('Y Label', fontsize=12)
ax.grid(True, alpha=0.3)
ax.legend(loc='best')

plt.tight_layout()
plt.show()
```

## 📈 Grouped Visualizations

### Grouped Bar Charts

```python
# Group by category
grouped = df.groupby('category')['value'].sum()
grouped.plot(kind='bar')
```

### Faceted Plots

```python
# Create faceted plots (requires seaborn)
sns.FacetGrid(df, col='category').map(plt.plot, 'date', 'value')
```

## 🔧 Integration with Matplotlib

### Using Matplotlib Directly

```python
# Create figure and axes
fig, ax = plt.subplots(figsize=(10, 6))

# Plot on axes
df.plot(ax=ax)

# Customize
ax.set_title('My Plot')
ax.set_xlabel('X')
ax.set_ylabel('Y')

plt.show()
```

### Combining Pandas and Matplotlib

```python
# Use pandas for data, matplotlib for customization
ax = df.plot(figsize=(10, 6))
ax.axhline(y=0, color='r', linestyle='--', linewidth=1)
ax.axvline(x=df.index[50], color='g', linestyle='--', linewidth=1)
plt.show()
```

## 📋 Module 8 Exercises

### Exercise 1: Basic Plots
1. Create line, bar, and scatter plots
2. Customize colors, labels, and titles
3. Save plots to files

### Exercise 2: Advanced Visualization
1. Create subplots with multiple charts
2. Create correlation heatmaps
3. Visualize time series data

### Exercise 3: Publication Quality
1. Create a polished visualization
2. Add proper labels, legends, and annotations
3. Export in high resolution

## 🔗 Additional Resources

- [Pandas Plotting](https://pandas.pydata.org/docs/user_guide/visualization.html)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- [Seaborn Documentation](https://seaborn.pydata.org/)

## ✅ Module 8 Checklist

Before moving to Module 9, ensure you can:

- [ ] Create basic plots with Pandas
- [ ] Customize plot appearance
- [ ] Create different chart types
- [ ] Use subplots effectively
- [ ] Integrate with Matplotlib/Seaborn
- [ ] Create publication-quality visualizations

---

**Next Module**: [Module 9: Performance Optimization](../09-performance-optimization/README.md)

