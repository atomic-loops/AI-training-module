# Module 2: Setting Up NumPy

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Install NumPy in different environments
- Configure your development environment for NumPy
- Import NumPy correctly and follow best practices
- Verify your installation and troubleshoot common issues

## 📦 Installation Methods

### Using pip (Recommended)

The simplest way to install NumPy:

```bash
pip install numpy
```

For a specific version:

```bash
pip install numpy==1.24.0
```

### Using conda

If you're using Anaconda or Miniconda:

```bash
conda install numpy
```

Or using conda-forge:

```bash
conda install -c conda-forge numpy
```

### Using pip with virtual environment (Best Practice)

Always use a virtual environment to avoid conflicts:

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Install NumPy
pip install numpy
```

## 🔧 Environment Setup

### Python Version Requirements

- **Minimum**: Python 3.8
- **Recommended**: Python 3.9 or higher
- NumPy supports Python 3.8 through 3.11

### Check Your Python Version

```bash
python --version
# or
python3 --version
```

### Verify NumPy Installation

```python
import numpy as np
print(np.__version__)
```

Expected output: `1.24.0` or similar version number

## 📝 Import Conventions

### Standard Import (Recommended)

```python
import numpy as np
```

This is the **universal convention** used by the entire data science community.

### Why `np`?

- **Short and clear**: Easy to type and read
- **Universal**: Everyone in the community uses it
- **Namespace**: Avoids conflicts with other libraries
- **Best practice**: Recommended by NumPy documentation

### Other Import Styles (Not Recommended)

```python
# Don't do this - pollutes namespace
from numpy import *

# Don't do this - too verbose
import numpy

# Don't do this - non-standard
import numpy as num
```

## 🛠️ IDE Configuration

### Jupyter Notebooks

NumPy works seamlessly with Jupyter:

```python
# In a Jupyter cell
import numpy as np
arr = np.array([1, 2, 3])
arr
```

### VS Code

1. Install Python extension
2. Create a `.vscode/settings.json`:
```json
{
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true
}
```

### PyCharm

1. Go to File → Settings → Project → Python Interpreter
2. Click `+` to add packages
3. Search for `numpy` and install

## ✅ Verification and Testing

### Basic Test

Create a test file `test_numpy.py`:

```python
import numpy as np

# Test array creation
arr = np.array([1, 2, 3, 4, 5])
print("Array:", arr)
print("Shape:", arr.shape)
print("Data type:", arr.dtype)

# Test basic operations
print("Sum:", arr.sum())
print("Mean:", arr.mean())
print("Max:", arr.max())

print("✅ NumPy is working correctly!")
```

Run it:

```bash
python test_numpy.py
```

### Performance Test

```python
import numpy as np
import time

# Create large array
arr = np.random.rand(1000000)

# Time an operation
start = time.time()
result = arr * 2
end = time.time()

print(f"Time taken: {end - start:.6f} seconds")
print("✅ Performance test passed!")
```

## 🐛 Troubleshooting

### Common Issues

#### Issue 1: Import Error

```
ModuleNotFoundError: No module named 'numpy'
```

**Solution:**
```bash
pip install numpy
# or
pip3 install numpy
```

#### Issue 2: Wrong Python Version

**Solution:** Ensure you're using Python 3.8 or higher

#### Issue 3: Installation Conflicts

**Solution:** Use a virtual environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install numpy
```

#### Issue 4: Permission Errors

**Solution:** Use `--user` flag or virtual environment

```bash
pip install --user numpy
```

## 📋 Module 2 Exercises

### Exercise 1: Installation
1. Install NumPy in a virtual environment
2. Verify the installation
3. Print the NumPy version

### Exercise 2: Import Test
Create a script that:
- Imports NumPy correctly
- Creates a simple array
- Performs a basic operation
- Prints the result

### Exercise 3: Environment Setup
Set up your preferred IDE (Jupyter, VS Code, or PyCharm) for NumPy development

## 🔗 Additional Resources

- [NumPy Installation Guide](https://numpy.org/install/)
- [NumPy User Guide - Quickstart](https://numpy.org/doc/stable/user/quickstart.html)
- [Python Virtual Environments](https://docs.python.org/3/tutorial/venv.html)

## ✅ Module 2 Checklist

Before moving to Module 3, ensure you can:

- [ ] Install NumPy successfully
- [ ] Import NumPy using the standard convention
- [ ] Verify your installation works
- [ ] Set up your development environment
- [ ] Troubleshoot common installation issues

---

**Next Module**: [Module 3: NumPy Essentials](../03-essentials/README.md)

