# Module 11: NumPy Integration with Other Libraries

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Integrate NumPy with Pandas
- Use NumPy with Matplotlib for visualization
- Combine NumPy with scikit-learn
- Work with NumPy in SciPy
- Understand NumPy's role in the data science ecosystem

## 🐼 NumPy and Pandas

### Converting Between NumPy and Pandas

```python
import numpy as np
import pandas as pd

# NumPy array to Pandas Series
arr = np.array([1, 2, 3, 4, 5])
series = pd.Series(arr)
print(series)

# NumPy array to Pandas DataFrame
arr_2d = np.array([[1, 2, 3], [4, 5, 6]])
df = pd.DataFrame(arr_2d, columns=['A', 'B', 'C'])
print(df)

# Pandas to NumPy
df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6]})
arr = df.values  # Returns NumPy array
# or
arr = df.to_numpy()  # Preferred method (Pandas 0.24+)
```

### Using NumPy Functions with Pandas

```python
# NumPy functions work with Pandas
df = pd.DataFrame({'A': [1, 2, 3, 4, 5], 'B': [6, 7, 8, 9, 10]})

# Apply NumPy functions
result = np.sqrt(df['A'])
result = np.mean(df.values)
result = np.sum(df, axis=0)
```

## 📊 NumPy and Matplotlib

### Basic Plotting

```python
import numpy as np
import matplotlib.pyplot as plt

# Create data with NumPy
x = np.linspace(0, 10, 100)
y = np.sin(x)

# Plot with Matplotlib
plt.plot(x, y)
plt.xlabel('X axis')
plt.ylabel('Y axis')
plt.title('Sine Wave')
plt.show()
```

### Multiple Plots

```python
# Create multiple arrays
x = np.linspace(0, 10, 100)
y1 = np.sin(x)
y2 = np.cos(x)
y3 = np.sin(x) * np.cos(x)

# Plot together
plt.plot(x, y1, label='sin(x)')
plt.plot(x, y2, label='cos(x)')
plt.plot(x, y3, label='sin(x)*cos(x)')
plt.legend()
plt.show()
```

### 2D Visualizations

```python
# Create 2D data
x = np.linspace(-5, 5, 100)
y = np.linspace(-5, 5, 100)
X, Y = np.meshgrid(x, y)
Z = np.sin(np.sqrt(X**2 + Y**2))

# Contour plot
plt.contour(X, Y, Z)
plt.colorbar()
plt.show()

# Heatmap
plt.imshow(Z, cmap='viridis')
plt.colorbar()
plt.show()
```

## 🤖 NumPy and scikit-learn

### Data Preparation

```python
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

# Create NumPy arrays
X = np.random.rand(100, 3)  # Features
y = np.random.rand(100)     # Target

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Train model (scikit-learn expects NumPy arrays)
model = LinearRegression()
model.fit(X_train, y_train)

# Predict
predictions = model.predict(X_test)
```

### Feature Engineering

```python
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA

# Standardize features
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)  # Input: NumPy array

# Dimensionality reduction
pca = PCA(n_components=2)
X_reduced = pca.fit_transform(X_scaled)  # Returns NumPy array
```

## 🔬 NumPy and SciPy

### Scientific Computing

```python
import numpy as np
from scipy import stats, optimize, integrate

# Statistics
data = np.random.normal(0, 1, 1000)
mean, std = stats.norm.fit(data)

# Optimization
def objective(x):
    return (x - 2)**2 + 1

result = optimize.minimize(objective, x0=0)
minimum = result.x  # NumPy array

# Integration
def func(x):
    return np.sin(x)

integral, error = integrate.quad(func, 0, np.pi)
```

### Linear Algebra with SciPy

```python
from scipy import linalg

# Create matrix
A = np.array([[1, 2], [3, 4]])

# Solve linear system
b = np.array([5, 6])
x = linalg.solve(A, b)

# Eigenvalue decomposition
eigenvals, eigenvecs = linalg.eig(A)

# SVD
U, s, Vt = linalg.svd(A)
```

## 🎨 NumPy and Image Processing

### Using PIL/Pillow

```python
from PIL import Image
import numpy as np

# Image to NumPy array
img = Image.open('image.jpg')
img_array = np.array(img)  # Shape: (height, width, channels)

# Process with NumPy
img_gray = np.mean(img_array, axis=2)  # Convert to grayscale
img_bright = img_array + 50  # Brighten image

# NumPy array to Image
img_processed = Image.fromarray(img_bright.astype(np.uint8))
img_processed.save('processed.jpg')
```

### Using OpenCV

```python
import cv2
import numpy as np

# Read image (returns NumPy array)
img = cv2.imread('image.jpg')  # BGR format

# Process with NumPy
img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
img_blur = cv2.GaussianBlur(img, (5, 5), 0)

# NumPy operations
edges = np.gradient(img_gray)
```

## 🧮 NumPy and SymPy

### Symbolic to Numeric

```python
import numpy as np
import sympy as sp

# Create symbolic expression
x = sp.Symbol('x')
expr = x**2 + 2*x + 1

# Convert to NumPy function
f = sp.lambdify(x, expr, 'numpy')

# Evaluate with NumPy array
x_vals = np.linspace(-5, 5, 100)
y_vals = f(x_vals)  # NumPy array
```

## 🔄 Data Interchange Formats

### NumPy and HDF5

```python
import h5py
import numpy as np

# Save NumPy array to HDF5
arr = np.random.rand(1000, 1000)
with h5py.File('data.h5', 'w') as f:
    f.create_dataset('array', data=arr)

# Load from HDF5
with h5py.File('data.h5', 'r') as f:
    loaded_arr = f['array'][:]  # Returns NumPy array
```

### NumPy and JSON

```python
import json
import numpy as np

# NumPy to JSON (convert to list first)
arr = np.array([1, 2, 3, 4, 5])
json_str = json.dumps(arr.tolist())

# JSON to NumPy
loaded = json.loads(json_str)
arr = np.array(loaded)
```

## 📋 Module 11 Exercises

### Exercise 1: Pandas Integration
1. Create a NumPy array and convert it to a Pandas DataFrame
2. Apply NumPy functions to Pandas data
3. Convert Pandas data back to NumPy

### Exercise 2: Visualization
1. Create NumPy arrays for x and y data
2. Plot the data using Matplotlib
3. Create a 2D visualization (contour or heatmap)

### Exercise 3: Machine Learning
1. Prepare data as NumPy arrays
2. Use scikit-learn to train a simple model
3. Make predictions and evaluate

## 🔗 Additional Resources

- [NumPy Ecosystem](https://numpy.org/ecosystem/)
- [Pandas NumPy Integration](https://pandas.pydata.org/docs/user_guide/basics.html#basics-dtypes)
- [Matplotlib NumPy Guide](https://matplotlib.org/stable/tutorials/introductory/pyplot.html)
- [scikit-learn Data Format](https://scikit-learn.org/stable/modules/preprocessing.html)

## ✅ Module 11 Checklist

Before completing the NumPy playbook, ensure you can:

- [ ] Convert between NumPy and Pandas
- [ ] Visualize NumPy arrays with Matplotlib
- [ ] Use NumPy arrays with scikit-learn
- [ ] Integrate NumPy with SciPy
- [ ] Work with images using NumPy
- [ ] Exchange data between NumPy and other formats

---

**Congratulations!** You've completed the NumPy playbook. Continue practicing and exploring advanced topics!

