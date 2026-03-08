# Module: Pandas Mastery (From Zero to Elite)

**Level:** Beginner → Elite  
**Time to Complete:** 60 Minutes (Reading + Practice)

---

## 📘 Part 1: What Are We Even Doing?

### What is Pandas?

**Pandas** is the ultimate data manipulation and analysis library in Python. If NumPy is the engine for fast math, Pandas is the dashboard for working with real-world tabular data (like Excel spreadsheets, SQL tables, or CSV files).

It introduces two main superpowers:

1. **Series**: A 1-dimensional column of data with custom labels (an index).
2. **DataFrame**: A 2-dimensional table of data (like an Excel sheet) made of multiple Series.

> **💡 The Golden Analogy:**  
> Imagine Python is a warehouse. **NumPy** is the forklift driving around doing heavy lifting fast. **Pandas** is the automated inventory system that labels, sorts, and organizes every box perfectly.

---

## 🟢 Level 1: Foundations (0 → Beginner)

_Goal: Loading data, viewing it, and understanding Series & DataFrames._

### 1. Creating and Loading Data

First, import Pandas (usually as `pd`).

```python
import pandas as pd

# 1. From a Dictionary (Creating a DataFrame manually)
data = {
    "Name": ["Alice", "Bob", "Charlie"],
    "Age": [25, 30, 35],
    "City": ["NYC", "LA", "Chicago"]
}
df = pd.DataFrame(data)

# 2. From a file (The most common way)
# df = pd.read_csv("data.csv")
# df = pd.read_excel("data.xlsx")
# df = pd.read_json("data.json")
```

### 2. Inspecting the DataFrame

Once you load a CSV, you need to look at it.

```python
print(df.head(2))    # Shows the first 2 rows
print(df.tail(2))    # Shows the last 2 rows
print(df.info())     # Shows column types, null values, and memory usage
print(df.describe()) # Shows summary statistics for numeric columns (mean, min, max, etc.)
print(df.columns)    # List of column names
```

### 3. Basic Selection

Accessing specific columns or rows.

```python
# Select a single column (returns a Pandas Series)
ages = df["Age"]     # or df.Age (if no spaces in name)

# Select multiple columns (returns a new DataFrame)
subset = df[["Name", "City"]]
```

---

## 🟡 Level 2: Engineering (Beginner → Intermediate)

_Goal: Data Selection, Cleaning, and Aggregation._

### 1. Advanced Selection (`loc` and `iloc`)

- `.loc[]` selects data by **label** (the actual index name or column name).
- `.iloc[]` selects data by **integer position** (the 0-based row/column number).

```python
# Using loc [row_label, column_label]
print(df.loc[0, "Name"])      # Gets "Alice"

# Using iloc [row_index, col_index]
print(df.iloc[0, 0])          # Gets "Alice" (0th row, 0th col)

# Slicing with loc
print(df.loc[0:2, ["Name", "Age"]]) # Rows 0 to 2, specific columns
```

### 2. Filtering (Boolean Indexing)

You usually want to find specific rows that match a condition.

```python
# Find everyone older than 28
older_than_28 = df[df["Age"] > 28]

# Multiple conditions: Use & (and), | (or), and wrap conditions in ()
nyc_or_old = df[(df["City"] == "NYC") | (df["Age"] >= 35)]
```

### 3. Data Cleaning (Handling Missing Values)

Real-world data is messy and has missing (`NaN`) values.

```python
# Add a messy row for example
df.loc[3] = ["David", None, "Miami"]

# 1. Check for nulls
print(df.isna().sum())

# 2. Drop rows with any null values
clean_df = df.dropna()

# 3. Fill null values with a specific number (like the mean)
mean_age = df["Age"].mean()
filled_df = df.fillna({"Age": mean_age})

# 4. Remove exact duplicate rows
no_dupes = df.drop_duplicates()
```

---

## 🟠 Level 3: Optimization & Logic (Intermediate → Advanced)

_Goal: Grouping, Merging, Transformations, and Time Series._

### 1. GroupBy & Aggregation

Summarizing data across categories (Exactly like a Pivot Table in Excel).

```python
# Assuming we have a 'Department' and 'Salary' column
# avg_salaries = df.groupby("Department")["Salary"].mean()

# Advanced aggregation: multiple metrics at once
# summary = df.groupby("Department").agg({
#     "Salary": ["mean", "max"],
#     "Age": "median"
# })
```

### 2. Merging & Concatenation

Combining multiple DataFrames together (like SQL Joins).

```python
df1 = pd.DataFrame({"ID": [1, 2], "Role": ["Engineer", "Designer"]})
df2 = pd.DataFrame({"ID": [1, 2], "Bonus": [5000, 3000]})

# Merge (SQL Join) based on the "ID" column
merged = pd.merge(df1, df2, on="ID", how="inner") # how can be 'left', 'right', 'outer', 'inner'

# Concat (Stacking them vertically or horizontally)
# vertically_stacked = pd.concat([df_january, df_february], axis=0)
```

### 3. Transformations (`apply` and `.str`)

Applying custom logic or text processing.

```python
# Using 'apply' with a lambda function
df["Age_In_10_Years"] = df["Age"].apply(lambda x: x + 10)

# String manipulation accessor (.str)
df["Name_Uppercase"] = df["Name"].str.upper()
df["Is_NYC"] = df["City"].str.contains("NYC")
```

### 4. Time Series Basics

Pandas was originally built for financial time series data.

```python
# Convert a string column to real Date/Time objects
# df["Date"] = pd.to_datetime(df["Date"])

# Set date as the index to enable resampling
# df.set_index("Date", inplace=True)

# Resample: Group daily data into Monthly averages
# monthly_average = df.resample("ME").mean()
```

---

## 🟣 Level 4: Elite Practices (Advanced → Elite)

_Goal: Memory Optimization, Vectorization over `apply`, and high-performance querying._

### 1. Memory Reduction via Dtypes

When loading millions of rows, Pandas defaults to heavy data types (like 64-bit integers and objects for strings). Downcasting saves incredible amounts of RAM.

```python
# Instead of 64-bit int, use 8-bit int if max value is < 127
df["Age"] = df["Age"].astype("int8")

# Turn low-cardinality strings (like "Male"/"Female" or "Department") into Categories
df["City"] = df["City"].astype("category")
# Memory can easily drop by 80% with categories!
```

### 2. The `.query()` and `.eval()` engines

For massive DataFrames (1M+ rows), Boolean masking (`df[df["Age"] > 30]`) creates heavy temporary arrays in memory. `query` uses `numexpr` C-backend to evaluate conditions faster and with less RAM.

```python
# Standard filtering involves intermediate arrays
# filtered = df[(df["Age"] > 30) & (df["City"] == "NYC")]

# .query is faster, reads like SQL, and uses less memory
filtered = df.query("Age > 30 and City == 'NYC'")
```

### 3. Avoiding `.apply()` for Vectorization

Beginners overuse `.apply()`. `.apply()` is just a hidden `for` loop in Python. It is **slow**. Always try to use Pandas built-in vectorized string or math methods instead.

```python
# ❌ Slow
# df["Cost"] = df.apply(lambda row: row["Price"] * row["Tax"], axis=1)

# ✅ Fast (Vectorized)
# df["Cost"] = df["Price"] * df["Tax"]
```

### 4. Polars / Chunking Awareness

When DataFrames exceed your local RAM (e.g., a 20GB CSV on a 16GB RAM laptop):

1. **Chunksize:** `pd.read_csv('huge.csv', chunksize=100000)` loads data in manageable blocks.
2. **Polars:** Modern data engineers often swap to the `polars` library (written in Rust) for extreme scale, as it utilizes multi-core processing automatically, unlike single-threaded Pandas.

---

## 🏁 Final Challenge

To complete this module:

1. Load a real `.csv` file from Kaggle using `pd.read_csv()`.
2. Find the total number of missing values across all columns.
3. Drop the rows with missing values.
4. Use `groupby` to find the mean of a numeric column grouped by a categorical column.
