# Module 2: Setting Up Pandas

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Install Pandas in different environments
- Configure your development environment for Pandas
- Import Pandas correctly and follow best practices
- Verify your installation and troubleshoot common issues

## 📦 Installation Methods

### Using pip (Recommended)

The simplest way to install Pandas:

```bash
pip install pandas
```

For a specific version:

```bash
pip install pandas==2.0.0
```

### Using conda

If you're using Anaconda or Miniconda:

```bash
conda install pandas
```

Or using conda-forge:

```bash
conda install -c conda-forge pandas
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

# Install Pandas
pip install pandas
```

## 🔧 Environment Setup

### Python Version Requirements

- **Minimum**: Python 3.8
- **Recommended**: Python 3.9 or higher
- Pandas 2.0+ requires Python 3.8+

### Dependencies

Pandas automatically installs:
- **NumPy**: Required for array operations
- **pytz**: For timezone support
- **dateutil**: For date parsing

### Check Your Python Version

```bash
python --version
# or
python3 --version
```

### Verify Pandas Installation

```python
import pandas as pd
print(pd.__version__)
```

Expected output: `2.0.0` or similar version number

## 📝 Import Conventions

### Standard Import (Recommended)

```python
import pandas as pd
```

This is the **universal convention** used by the entire data science community.

### Why `pd`?

- **Short and clear**: Easy to type and read
- **Universal**: Everyone in the community uses it
- **Namespace**: Avoids conflicts with other libraries
- **Best practice**: Recommended by Pandas documentation

### Other Import Styles (Not Recommended)

```python
# Don't do this - pollutes namespace
from pandas import *

# Don't do this - too verbose
import pandas

# Don't do this - non-standard
import pandas as p
```

## 🛠️ IDE Configuration

### Jupyter Notebooks

Pandas works seamlessly with Jupyter:

```python
# In a Jupyter cell
import pandas as pd
df = pd.DataFrame({'A': [1, 2, 3]})
df
```

### VS Code

1. Install Python extension
2. Install Jupyter extension for notebook support
3. Create a `.vscode/settings.json`:
```json
{
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "jupyter.askForKernelRestart": false
}
```

### PyCharm

1. Go to File → Settings → Project → Python Interpreter
2. Click `+` to add packages
3. Search for `pandas` and install

## ✅ Verification and Testing

### Basic Test

Create a test file `test_pandas.py`:

```python
import pandas as pd

# Test DataFrame creation
data = {'Name': ['Alice', 'Bob'], 'Age': [25, 30]}
df = pd.DataFrame(data)
print("DataFrame:")
print(df)
print("\nShape:", df.shape)
print("Columns:", df.columns.tolist())

# Test basic operations
print("\nMean age:", df['Age'].mean())
print("✅ Pandas is working correctly!")
```

Run it:

```bash
python test_pandas.py
```

### Data Loading Test

```python
import pandas as pd

# Test reading CSV (create a simple test file first)
# Create test.csv with: name,age\nAlice,25\nBob,30
df = pd.read_csv('test.csv')
print(df)
print("✅ Data loading works!")
```

## 🐛 Troubleshooting

### Common Issues

#### Issue 1: Import Error

```
ModuleNotFoundError: No module named 'pandas'
```

**Solution:**
```bash
pip install pandas
# or
pip3 install pandas
```

#### Issue 2: Wrong Python Version

**Solution:** Ensure you're using Python 3.8 or higher

#### Issue 3: Installation Conflicts

**Solution:** Use a virtual environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install pandas
```

#### Issue 4: Missing Dependencies

**Solution:** Reinstall with dependencies

```bash
pip install --upgrade pandas
```

#### Issue 5: Excel File Support

If you need to read Excel files:

```bash
pip install openpyxl  # For .xlsx files
pip install xlrd      # For .xls files
```

## 📋 Module 2 Exercises

### Exercise 1: Installation
1. Install Pandas in a virtual environment
2. Verify the installation
3. Print the Pandas version

### Exercise 2: Import Test
Create a script that:
- Imports Pandas correctly
- Creates a simple DataFrame
- Performs a basic operation
- Prints the result

### Exercise 3: Environment Setup
Set up your preferred IDE (Jupyter, VS Code, or PyCharm) for Pandas development

## 🔗 Additional Resources

- [Pandas Installation Guide](https://pandas.pydata.org/docs/getting_started/install.html)
- [Pandas User Guide - Getting Started](https://pandas.pydata.org/docs/user_guide/getting_started.html)
- [Python Virtual Environments](https://docs.python.org/3/tutorial/venv.html)

## ✅ Module 2 Checklist

Before moving to Module 3, ensure you can:

- [ ] Install Pandas successfully
- [ ] Import Pandas using the standard convention
- [ ] Verify your installation works
- [ ] Set up your development environment
- [ ] Troubleshoot common installation issues

---

**Next Module**: [Module 3: Pandas Essentials](../03-essentials/README.md)

