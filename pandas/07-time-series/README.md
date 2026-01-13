# Module 7: Time Series with Pandas

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Work with datetime data in Pandas
- Create and manipulate time series
- Resample time series data
- Handle time zones
- Perform time-based indexing and slicing
- Calculate time-based aggregations

## 📅 Working with Datetime

### Creating Datetime Objects

```python
import pandas as pd
import numpy as np

# From strings
dates = pd.to_datetime(['2023-01-01', '2023-01-02', '2023-01-03'])

# From various formats
pd.to_datetime('01/01/2023', format='%d/%m/%Y')
pd.to_datetime('2023-01-01 12:00:00')

# Create date range
date_range = pd.date_range('2023-01-01', periods=10, freq='D')
date_range = pd.date_range('2023-01-01', '2023-12-31', freq='D')
```

### Datetime Index

```python
# Create DataFrame with datetime index
df = pd.DataFrame({
    'value': np.random.randn(100)
}, index=pd.date_range('2023-01-01', periods=100, freq='D'))

# Set datetime as index
df = pd.DataFrame({
    'date': pd.date_range('2023-01-01', periods=100, freq='D'),
    'value': np.random.randn(100)
})
df = df.set_index('date')
```

## 🔄 Time Series Operations

### Time-Based Indexing

```python
# Select by year
df['2023']

# Select by year and month
df['2023-01']

# Select date range
df['2023-01-01':'2023-01-31']

# Select specific date
df.loc['2023-01-15']
```

### Time-Based Slicing

```python
# Slice by time
df.loc['2023-01-01':'2023-03-31']  # Q1
df.loc['2023-06-01':'2023-08-31']  # Q3

# Using partial datetime strings
df.loc['2023-01']  # January 2023
df.loc['2023']     # Year 2023
```

## 📊 Resampling

### Downsampling (Lower Frequency)

```python
# Daily to monthly
df.resample('M').sum()   # Monthly sum
df.resample('M').mean()  # Monthly mean

# Daily to weekly
df.resample('W').sum()

# Daily to quarterly
df.resample('Q').sum()

# Custom aggregation
df.resample('M').agg(['sum', 'mean', 'std'])
```

### Upsampling (Higher Frequency)

```python
# Monthly to daily
monthly = df.resample('M').sum()
monthly.resample('D').ffill()  # Forward fill
monthly.resample('D').bfill()  # Backward fill
monthly.resample('D').interpolate()  # Interpolate
```

### Resampling Methods

```python
# Aggregation methods
df.resample('M').sum()
df.resample('M').mean()
df.resample('M').max()
df.resample('M').min()
df.resample('M').std()
df.resample('M').count()

# First and last
df.resample('M').first()
df.resample('M').last()

# Custom function
df.resample('M').apply(lambda x: x.max() - x.min())
```

## 🕐 Time Frequencies

### Common Frequencies

```python
# Time frequencies
'D'   # Daily
'W'   # Weekly
'M'   # Month end
'MS'  # Month start
'Q'   # Quarter end
'QS'  # Quarter start
'A'   # Year end
'AS'  # Year start
'H'   # Hourly
'T'   # Minutely
'S'   # Secondly

# Examples
pd.date_range('2023-01-01', periods=10, freq='D')   # Daily
pd.date_range('2023-01-01', periods=10, freq='H')   # Hourly
pd.date_range('2023-01-01', periods=10, freq='M')   # Monthly
```

### Custom Frequencies

```python
# Business days
pd.date_range('2023-01-01', periods=10, freq='B')

# Business month end
pd.date_range('2023-01-01', periods=10, freq='BM')

# Custom offset
from pandas.tseries.offsets import MonthEnd
df.resample(MonthEnd()).sum()
```

## 🌍 Time Zones

### Working with Time Zones

```python
# Create timezone-aware datetime
dates = pd.date_range('2023-01-01', periods=5, freq='D', tz='UTC')

# Convert timezone
dates_utc = pd.date_range('2023-01-01', periods=5, freq='D', tz='US/Eastern')
dates_utc.tz_convert('UTC')

# Localize naive datetime
naive = pd.date_range('2023-01-01', periods=5, freq='D')
naive.tz_localize('US/Eastern')

# Remove timezone
dates_utc.tz_localize(None)
```

## 📈 Time Series Analysis

### Rolling Windows

```python
# Rolling mean
df['value'].rolling(window=7).mean()   # 7-day rolling mean
df['value'].rolling(window=30).mean()  # 30-day rolling mean

# Rolling sum
df['value'].rolling(window=7).sum()

# Rolling statistics
df['value'].rolling(window=7).std()
df['value'].rolling(window=7).min()
df['value'].rolling(window=7).max()

# Expanding window
df['value'].expanding().mean()
df['value'].expanding().sum()
```

### Shifting and Lagging

```python
# Shift forward (lag)
df['value_lag1'] = df['value'].shift(1)   # Previous day
df['value_lag7'] = df['value'].shift(7)   # 7 days ago

# Shift backward (lead)
df['value_lead1'] = df['value'].shift(-1)  # Next day

# Percentage change
df['value_pct_change'] = df['value'].pct_change()
df['value_pct_change_7d'] = df['value'].pct_change(periods=7)
```

### Time Differences

```python
# Calculate time differences
df.index.to_series().diff()  # Time between rows

# Time since start
(df.index - df.index[0]).days  # Days since start

# Time until next
(df.index.shift(-1) - df.index).days  # Days until next
```

## 🎯 Time-Based Grouping

### Group by Time Periods

```python
# Group by year
df.groupby(df.index.year).sum()

# Group by month
df.groupby(df.index.month).sum()

# Group by day of week
df.groupby(df.index.dayofweek).mean()

# Group by custom periods
df.groupby(pd.Grouper(freq='M')).sum()
df.groupby(pd.Grouper(freq='Q')).mean()
```

### Extracting Time Components

```python
# Extract components
df.index.year
df.index.month
df.index.day
df.index.dayofweek  # 0=Monday, 6=Sunday
df.index.dayofyear
df.index.quarter
df.index.week
df.index.isocalendar()

# Add as columns
df['year'] = df.index.year
df['month'] = df.index.month
df['day_of_week'] = df.index.dayofweek
```

## 📊 Practical Examples

### Stock Price Analysis

```python
# Load stock data (example)
prices = pd.DataFrame({
    'price': np.random.randn(100).cumsum() + 100
}, index=pd.date_range('2023-01-01', periods=100, freq='D'))

# Calculate returns
prices['returns'] = prices['price'].pct_change()

# Rolling statistics
prices['ma_7'] = prices['price'].rolling(7).mean()
prices['ma_30'] = prices['price'].rolling(30).mean()

# Volatility
prices['volatility'] = prices['returns'].rolling(30).std()
```

### Sales Analysis

```python
# Daily sales
sales = pd.DataFrame({
    'sales': np.random.randint(1000, 5000, 365)
}, index=pd.date_range('2023-01-01', periods=365, freq='D'))

# Monthly totals
monthly = sales.resample('M').sum()

# Weekly averages
weekly = sales.resample('W').mean()

# Year-over-year comparison
sales['year'] = sales.index.year
sales['month'] = sales.index.month
yearly_comparison = sales.groupby(['year', 'month']).sum()
```

## 📋 Module 7 Exercises

### Exercise 1: Datetime Operations
1. Create a time series with datetime index
2. Extract time components (year, month, day)
3. Filter data by time ranges

### Exercise 2: Resampling
1. Resample daily data to monthly
2. Resample monthly data to daily (with interpolation)
3. Calculate rolling statistics

### Exercise 3: Time Series Analysis
1. Calculate percentage changes
2. Create lagged variables
3. Perform time-based grouping

## 🔗 Additional Resources

- [Pandas Time Series](https://pandas.pydata.org/docs/user_guide/timeseries.html)
- [Pandas Datetime](https://pandas.pydata.org/docs/user_guide/timeseries.html#time-date-components)
- [Time Series Analysis](https://pandas.pydata.org/docs/user_guide/timeseries.html#resampling)

## ✅ Module 7 Checklist

Before moving to Module 8, ensure you can:

- [ ] Create and work with datetime objects
- [ ] Use datetime as index
- [ ] Resample time series data
- [ ] Handle time zones
- [ ] Perform time-based indexing and slicing
- [ ] Calculate rolling statistics and time differences
- [ ] Group data by time periods

---

**Next Module**: [Module 8: Data Visualization](../08-data-visualization/README.md)

