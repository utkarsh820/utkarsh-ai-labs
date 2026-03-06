# FunctionTransformer (Custom Pipelines)

**Level:** Intermediate → Advanced  
**Time to Complete:** 20 Minutes (Reading + Practice)

---

## 📘 Part 1: The Problem with Custom Code

You just learned about `Pipelines`. They are incredibly powerful, but they have a strict rule: **Everything inside a Pipeline must be a valid Scikit-Learn transformer** (meaning it contains an official `.fit()` and `.transform()` method).

What happens when Scikit-Learn doesn't have the mathematical function you need?

- What if you want to extract the length of a string column?
- What if you want to take the logarithm (`np.log`) of a skewed numeric column?
- What if you want to multiply two columns together?

You can't just throw `np.log` into a `Pipeline`. It will crash. This is where `FunctionTransformer` saves the day.

---

## 🟢 Level 1: The Foundation (`FunctionTransformer`)

**What it is:** A wrapper that turns any standard Python function or Numpy function into a legitimate Scikit-Learn Transformer.

```python
import numpy as np
from sklearn.preprocessing import FunctionTransformer
from sklearn.pipeline import Pipeline

# 1. Create a dummy dataset
import pandas as pd
df = pd.DataFrame({'Income': [1000, 50000, 1000000]})

# 2. Wrap the numpy log function
log_transformer = FunctionTransformer(np.log1p) # log1p handles zeroes better than log

# 3. Now you can use it in a pipeline!
pipe = Pipeline([
    ('log_transform', log_transformer)
])

print(pipe.fit_transform(df))
# All incomes are safely converted to orders of magnitude
```

---

## 🟡 Level 2: Custom Python Functions

Sometimes you need entirely custom logic (like text parsing).

You can define a standard python `def` function, but it MUST accept a multidimensional array (like a DataFrame or Numpy 2D array) and return an array of the same shape.

```python
def extract_ticket_prefix(df):
    """ Extracts the first letter of a ticket string, or 'X' if none exists """
    # Return a copy to avoid SettingWithCopy warnings in pandas
    df_out = df.copy()
    df_out['Ticket_Prefix'] = df_out['Ticket'].astype(str).str[0]
    return df_out[['Ticket_Prefix']] # return a 2D frame

# Wrap it!
# validate=False tells sklearn not to force it into a numpy float array (keep it as pandas text)
ticket_transformer = FunctionTransformer(extract_ticket_prefix, validate=False)

# Test it
df = pd.DataFrame({'Ticket': ['A123', 'B999', 456]})
print(ticket_transformer.transform(df))
```

---

## 🟠 Level 3: Stateless vs. Stateful

**This is the most critical concept to understand about FunctionTransformer.**

### What is a "Stateful" Transformer?

`StandardScaler` is **Stateful**. During the `.fit()` step, it calculates the Mean and Standard Deviation, and _remembers_ them. When `.transform()` is called on the Test Set, it applies those remembered values mapping exactly to the Training Data.

### What is a "Stateless" Transformer?

`FunctionTransformer` is **Stateless**. It has no memory. It does not learn anything during `.fit()`. It just blindly applies the mathematical function (like `np.log`) whenever `.transform()` is called.

**Why does this matter?**
If your custom function relies on the _entire column's statistics_ (like "divide everything by the column's maximum value"), you **cannot** use `FunctionTransformer` effectively inside cross-validation, because it will calculate a new Maximum value during the Test set transformation, causing Data Leakage!

If your function only looks at a _single row independently_ (like `np.log(X)` or `string.upper()`), `FunctionTransformer` is perfect.

---

## 🏁 Academy Exercise

**Task:**

1. Create a simple DataFrame containing a column called `"Area"` with right-skewed values (e.g., `[10, 100, 500, 10000, 50000]`).
2. Define a custom python function that divides all inputs by 10 (converting square feet to roughly square meters).
3. Wrap your custom function in a `FunctionTransformer`.
4. Apply the `.transform()` method to your DataFrame and print the result.
