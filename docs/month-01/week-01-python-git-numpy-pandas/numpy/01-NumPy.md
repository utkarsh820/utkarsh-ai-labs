# Module: NumPy Mastery (From Zero to Elite)

**Level:** Beginner → Elite  
**Time to Complete:** 45 Minutes (Reading + Practice)

---

## 📘 Part 1: What Are We Even Doing?

### What is NumPy?

**NumPy** (Numerical Python) is the foundation of numerical computing in Python. It provides the **ndarray** (N-dimensional array), a highly optimized, fast, and memory-efficient data structure for mathematical operations.

Unlike standard Python lists, which can hold mixed data types and are scattered in memory, **NumPy arrays** are homogeneous (same data type) and stored in contiguous memory blocks. This allows NumPy to utilize compiled C/Fortran code and **Vectorization** under the hood.

> **💡 The Golden Analogy:**  
> **Python Lists** are like a mixed box of random items (heavy, slow to find things).  
> **NumPy Arrays** are like an organized grid of identical items (lightweight, lightning fast to process).

---

## 🟢 Level 1: Foundations (0 → Beginner)

_Goal: Arrays, indexing, basic math, and understanding the core structure._

### 1. Creating Arrays

First, you always import NumPy as `np`.

```python
import numpy as np

# 1D Array from a list
arr_1d = np.array([1, 2, 3, 4, 5])

# 2D Array (Matrix)
arr_2d = np.array([[1, 2, 3], [4, 5, 6]])

# Built-in generator functions
zeros = np.zeros((3, 3))       # 3x3 matrix of 0.0
ones = np.ones((2, 4))         # 2x4 matrix of 1.0
sequence = np.arange(0, 10, 2) # [0, 2, 4, 6, 8]
spaced_out = np.linspace(0, 1, 5) # 5 values equally spaced between 0 and 1
```

### 2. Basic Indexing & Slicing

Getting data out of arrays works similarly to Python lists, but extended for multiple dimensions (commas separate dimensions).

```python
print(arr_1d[0])        # First element: 1
print(arr_1d[1:4])      # Slice: [2, 3, 4]

# For a 2D array [row, col]
print(arr_2d[0, 1])     # Row 0, Column 1: 2
print(arr_2d[:, 1])     # All rows, Column 1: [2, 5]
```

### 3. Basic Math & Random Numbers

NumPy handles math element-wise by default.

```python
a = np.array([10, 20, 30])
b = np.array([1, 2, 3])

print(a + b)  # [11, 22, 33]
print(a * b)  # [10, 40, 90]

# Generating basic random numbers
rand_nums = np.random.rand(3)         # 3 random floats between 0 and 1
rand_ints = np.random.randint(1, 10, 5) # 5 random ints between 1 and 9
```

---

## 🟡 Level 2: Engineering (Beginner → Intermediate)

_Goal: Data Manipulation, aggregations, boolean masking, and intermediate math._

### 1. Array Manipulation & Shaping

You often need to change the physical shape of your data (e.g., flattening an image into a 1D array for a neural network).

```python
matrix = np.arange(12)  # [0, 1, ... 11]

# Reshape into 3 rows, 4 columns
reshaped = matrix.reshape((3, 4))

# Flatten back to 1D
flat = reshaped.flatten()

# Transpose (swap rows and columns)
transposed = reshaped.transpose() # or reshaped.T

# Concatenation and Stacking
a = np.array([1, 2])
b = np.array([3, 4])
combined = np.concatenate((a, b)) # [1, 2, 3, 4]
stacked = np.stack((a, b))        # [[1, 2], [3, 4]]
```

### 2. Aggregations (Axis Logic)

When summing or averaging 2D arrays, **axis=0** applies vertically (down columns), and **axis=1** applies horizontally (across rows).

```python
data = np.array([[1, 2], [3, 4]])
# data is:
# [1, 2]
# [3, 4]

print(np.sum(data))          # Total sum: 10
print(np.mean(data, axis=0)) # Column means: [2.0, 3.0]
print(np.max(data, axis=1))  # Row maxes: [2, 4]
```

### 3. Boolean Masking & Fancy Indexing

Selecting elements based on conditions—crucial for data cleaning.

```python
arr = np.array([10, 50, 80, 20, 90])

# The Mask
mask = arr > 40
print(mask) # [False, True, True, False, True]

# Applying the mask to filter the array
filtered = arr[mask]   # [50, 80, 90]
# Shorthand: arr[arr > 40]

# Fancy indexing (passing a list of indices)
indices = [0, 2, 4]
print(arr[indices])    # [10, 80, 90]
```

---

## 🟠 Level 3: Optimization & Internals (Intermediate → Advanced)

_Goal: Broadcasting, vectorization logic, and complex linear algebra._

### 1. Broadcasting Rules

Broadcasting is how NumPy handles arrays of different shapes during math operations without actually making multiple copies in memory.

```python
matrix = np.ones((3, 3)) # 3x3 of 1s
vector = np.array([1, 2, 3])

# Vector is "broadcast" across each row of the matrix automatically
result = matrix + vector
# [[2.0, 3.0, 4.0],
#  [2.0, 3.0, 4.0],
#  [2.0, 3.0, 4.0]]
```

> **🧠 Concept:** For broadcasting to work, dimensions moving from right to left must either be **equal**, or one of them must be **1**.

### 2. Linear Algebra Operations

Fundamental for Machine Learning operations (like Forward Passes in Neural Networks).

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# Dot Product / Matrix Multiplication
# Note: A * B is element-wise. Use np.dot or the @ operator for true matmul.
product = A @ B
# equivalently: np.dot(A, B) or np.matmul(A, B)

# Inverses and Determinants
A_inv = np.linalg.inv(A)
det = np.linalg.det(A)
```

### 3. Advanced Manipulations (Expanding & Squeezing)

Sometimes ML frameworks (like PyTorch or TensorFlow) require specific dimension structures (like a "batch" dimension).

```python
arr = np.array([1, 2, 3]) # Shape (3,)

# Expand dimension (add a fake grouping axis)
expanded = np.expand_dims(arr, axis=0) # Shape (1, 3) --> [[1, 2, 3]]

# Squeeze (remove axes of length 1)
squeezed = np.squeeze(expanded)        # Shape (3,) --> [1, 2, 3]
```

---

## 🟣 Level 4: Elite Practices (Advanced → Elite)

_Goal: Understanding memory layout, C-interoperability, and extreme optimization._

### 1. Universal Functions (UFuncs) & Memory Views

UFuncs (`np.sin`, `np.exp`, etc.) execute loops in compiled C code. Writing a Python `for` loop over a NumPy array defeats the purpose of NumPy. Always vectorize.

```python
import time
large_arr = np.random.rand(10_000_000)

# ❌ Slow (Python Loop)
start = time.time()
res1 = [x**2 for x in large_arr]
print("Loop time:", time.time() - start) # ~2.5 seconds

# ✅ Fast (UFunc Vectorization)
start = time.time()
res2 = large_arr ** 2
print("Vectorized time:", time.time() - start) # ~0.02 seconds (100x faster)
```

### 2. Einsum (Einstein Summation)

`np.einsum` is the god-tier function of NumPy. It allows you to specify complex tensor operations in a single, highly optimized memory pass.

```python
A = np.random.rand(3, 3)
B = np.random.rand(3, 3)

# Instead of np.trace(np.dot(A, B))
# Compute trace of dot product elegantly:
trace = np.einsum('ij,ji->', A, B)
```

### 3. Memory Layout (C vs. Fortran Order)

NumPy arrays are stored continuously in RAM. By default, they use **C-order** (Row-major: row items are next to each other in memory). **F-order** (Fortran-order) means columns are continuous.

```python
# Create an array with explicit Fortran ordering
f_arr = np.array([[1, 2], [3, 4]], order='F')

# Accessing columns of f_arr is slightly faster than accessing rows,
# because of CPU cache locality.
```

### 4. Advanced Interoperability

NumPy arrays use the standard Python Buffer Protocol. This is why you can instantly convert a NumPy array into a PyTorch tensor (or vice versa) without copying the underlying memory. They share the same RAM pointer!

```python
# Typical in ML pipelines
import torch
np_array = np.array([1, 2, 3])
tensor = torch.from_numpy(np_array) # Zero-copy conversion!
```

---

## 🏁 Final Challenge

To complete this module:

1. Initialize a 5x5 matrix of random integers between 1 and 100.
2. Replace all numbers greater than 50 with `0`. (Hint: Boolean Masking).
3. Compute the `np.mean` of each column in your modified matrix.
