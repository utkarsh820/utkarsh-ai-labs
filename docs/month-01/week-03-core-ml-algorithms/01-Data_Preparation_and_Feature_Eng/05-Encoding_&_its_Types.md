# Categorical Encoding (From Zero to Elite)

**Level:** Beginner → Elite  
**Time to Complete:** 45 Minutes (Reading + Practice)

---

## 📘 Part 1: The "Why" of Encoding

### Why do we encode data?

Machine learning algorithms only understand numbers. They are fundamentally mathematical equations mapping inputs ($X$) to an output ($Y$). If you feed an algorithm a dataset with a column like `"City" = "New York"`, it crashes. It cannot multiply or subtract the string `"New York"`.

**Encoding** is the process of translating text (Categorical Data) into numbers in a way that respects the underlying logic of the data, so the model can learn from it.

### The Two Types of Categories

Before encoding, you must ask: _Does this text have a natural order?_

1. **Ordinal Data (Has an Order):** `["Low", "Medium", "High"]` or `["B.A.", "M.S.", "Ph.D."]`. There is a clear mathematical ranking here.
2. **Nominal Data (No Order):** `["Red", "Green", "Blue"]` or `["New York", "London", "Tokyo"]`. Is London mathematically "greater" than Tokyo? No.

---

## 🟢 Level 1: The Foundation (Beginner)

### 1. Label/Ordinal Encoding

**What it does:** Assigns a unique integer to each category based on an order.

- **Logic:** `"Small" = 1`, `"Medium" = 2`, `"Large" = 3`.
- **When to use:** ONLY use this for **Ordinal Data**. If you use this for Nominal data (like Cities: `NY=1, LA=2, Chicago=3`), the algorithm will wrongly assume that Chicago is mathematically "larger" or "worth more" than New York.

```python
import pandas as pd

df = pd.DataFrame({'Size': ['Small', 'Medium', 'Large', 'Medium']})

# Defining the exact order is crucial
size_map = {'Small': 1, 'Medium': 2, 'Large': 3}
df['Size_Encoded'] = df['Size'].map(size_map)
```

### 2. One-Hot Encoding (Dummy Variables)

**What it does:** Creates a completely new binary column (0 or 1) for _every_ unique category.

- **Logic:** If the `City` column has `NY`, `LA`, and `Chicago`, it makes three new columns: `is_NY`, `is_LA`, `is_Chicago`.
- **When to use:** The absolute standard for **Nominal Data** with a low number of unique categories (usually < 15 unique values).

```python
import pandas as pd

df = pd.DataFrame({'City': ['NY', 'LA', 'Chicago', 'NY']})

# Creates binary columns. drop_first=True avoids multicollinearity!
df_encoded = pd.get_dummies(df, columns=['City'], drop_first=True)
# Resulting columns: City_Chicago, City_NY (LA is dropped)
```

> **⚠️ The Dummy Variable Trap:** Why `drop_first=True`? If you have `is_Male` and `is_Female` columns, they are perfectly correlated. If `is_Male` is 0, the model instantly knows `is_Female` must be 1. This perfect correlation ("collinearity") makes linear models (like Linear Regression) mathematically unstable. We drop one column to break the trap.

---

## 🟡 Level 2: The "High Cardinality" Problem (Intermediate)

**"Cardinality"** refers to the number of unique categories in a column.

- Gender = Low Cardinality (2-3)
- US States = Medium Cardinality (50)
- ZIP Codes = **High Cardinality** (40,000+)

If you One-Hot Encode 40,000 ZIP codes, your dataset suddenly has 40,000 new columns. Your memory will crash, and your model will suffer from the "Curse of Dimensionality" (too wide, not enough depth to learn).

### 3. Frequency / Count Encoding

**What it does:** Replaces the category string with the number of times it appears in the dataset.

- **Logic:** If `"New York"` appears 5,000 times, replace the string `"New York"` with `5000`.
- **When to use:** Great for Tree-Based models (Random Forest, XGBoost) dealing with high cardinality. It assumes that the _rarity_ or _commonness_ of a category has predictive power.

```python
df = pd.DataFrame({'City': ['NY', 'NY', 'LA', 'Chicago', 'NY', 'LA']})

# Calculate frequencies
counts = df['City'].value_counts()
# Map counts back to the dataframe
df['City_Freq'] = df['City'].map(counts)
# NY becomes 3, LA becomes 2, Chicago becomes 1
```

### 4. Target / Mean Encoding

**What it does:** Replaces the category with the **average value of the target variable** for that specific category.

- **Logic:** If the goal is to predict "House Price" (Target), and the average house price in "New York" is $800,000, replace the string `"New York"` with `800000`.
- **When to use:** Incredibly powerful for Kaggle competitions and High Cardinality nominal data.
- **Warning:** Highly prone to **Data Leakage / Overfitting** if not done properly (you must calculate the mean using Cross-Validation, not the entire dataset).

```python
# Usually done via the category_encoders library
import category_encoders as ce

encoder = ce.TargetEncoder(cols=['City'])
# df['City_Target_Encoded'] = encoder.fit_transform(df['City'], df['House_Price'])
```

---

## 🟠 Level 3: Niche Compressors (Advanced)

What if you have massive cardinality, but you don't want to use Target Encoding for fear of data leakage?

### 5. Binary Encoding & BaseN Encoding

**What it does:** It assigns an integer to the category (like Label Encoding), converts that integer into a **Binary string** (e.g., `5` becomes `101`), and then splits those binary digits into separate columns.

- **Logic:** Instead of creating 100 One-Hot columns for 100 cities, it creates $\log_2(100) \approx 7$ columns.
- **When to use:** A fantastic compromise. It saves immense memory on features with hundreds of unique values while providing enough structure for tree-based models to split on.

```python
import category_encoders as ce

encoder = ce.BinaryEncoder(cols=['City'])
# df_binary = encoder.fit_transform(df['City'])
# Instead of 100 columns, you get City_0, City_1, City_2... City_7
```

### 6. Feature Hashing (The Hashing Trick)

**What it does:** Uses a hashing algorithm (like MD5 or MurmurHash) to convert strings into a fixed, pre-defined number of columns.

- **Logic:** "User_IP_192.168.1.1" goes through a hash function and lands in "Bucket #4". "User_IP_10.0.0.5" lands in "Bucket #2".
- **When to use:** **Extreme** scenarios. E.g., Ad-Click prediction processing 10 million unique IP addresses in real-time. You can't keep a dictionary of 10 million mappings in RAM. Hash them into 1,000 fixed columns.
- **Downside:** "Collisions." Sometimes completely unrelated strings will hash into the same exact bucket, diluting the data. Furthermore, you cannot reverse the hash to know what the original string was.

```python
import category_encoders as ce

# Force arbitrarily large unique strings into exactly 8 columns
encoder = ce.HashingEncoder(cols=['IP_Address'], n_components=8)
```

---

## 🟣 Level 4: The Deep Learning Frontier (Elite)

### 7. Entity Embeddings (Embedding Layers)

**What it does:** Takes high-cardinality categories and maps them into N-dimensional continuous space, where the Neural Network dynamically learns the relationships.

- **Logic:** Similar to Word2Vec in NLP (where "King" and "Queen" land near each other in space). Here, the model might figure out that "New York" and "San Francisco" are mathematically near each other because they behave similarly regarding house prices.
- **When to use:** The absolute state-of-the-art for tabular Deep Learning data with hundreds of categories (e.g., store ID, product ID). Popularized in Kaggle's Rossmann Store Sales competition.

```python
# Conceptual PyTorch Example
import torch.nn as nn

# 1000 unique cities, mapped to a dense 10-dimensional vector
city_embedding = nn.Embedding(num_embeddings=1000, embedding_dim=10)
```

---

## 📋 The Master "Which Encoder to Use?" Matrix

| Method                | Best For...                        | Used By...         | Pros                                     | Cons                                                |
| :-------------------- | :--------------------------------- | :----------------- | :--------------------------------------- | :-------------------------------------------------- |
| **Ordinal / Label**   | Ordered Data (Low/Med/High)        | All Models         | Simple, maintains order                  | Ruins nominal (unordered) data                      |
| **One-Hot / Dummies** | Unordered Data (Low Cardinality)   | Linear, SVM, Trees | Preserves strict independence            | Memory explosion if Cardinality is high             |
| **Count / Frequency** | High Cardinality                   | Trees / Forests    | Solves memory limits                     | Assumes rarity matters; ties cause collisions       |
| **Target Encoding**   | High Cardinality + Complex targets | Trees / Boosting   | Extremely powerful predictive signal     | Massive risk of overfitting / data leakage          |
| **Binary/BaseN**      | Mid-to-High Cardinality            | Trees / Boosting   | Great memory/performance compromise      | Math logic is slightly abstracted from reality      |
| **Hashing**           | Extreme Cardinality (Streaming)    | Real-time models   | Ultra-low memory footprint               | "Collisions" happen, impossible to reverse engineer |
| **Embeddings**        | Tabular Deep Learning              | Neural Networks    | Captures deep, complex sub-relationships | Slow to train, requires Deep Learning architecture  |

---

## 🏁 Academy Exercise

**Task:**

1. Load a dataset with a column containing states (e.g., 50 unique US states).
2. Apply `pd.get_dummies()` and observe the `df.shape`. How many columns did you add?
3. Install `category_encoders` (`pip install category_encoders`).
4. Apply a `BinaryEncoder` to the exact same column. Observe the `df.shape`. How much column space did you save compared to One-Hot?
5. **Bonus:** Apply a `TargetEncoder` grouping by State to predict a numerical column (like Salary). Look at resulting values!
