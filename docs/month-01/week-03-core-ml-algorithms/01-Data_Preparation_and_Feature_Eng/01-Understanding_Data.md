
### **Understanding Your Data (The First 7 Questions)**

#### **Objective**

To teach students how to perform a preliminary analysis of a dataset using Pandas before diving into visualization or modeling.

---

### **1. How big is the data?**

Before processing, you must know the volume of the data you are handling.

* **Method:** `df.shape`
* **Insight:** Returns the number of rows and columns. This helps you decide if the data fits in memory or if you need distributed processing.

### **2. How does the data look?**

Get a feel for the actual values and formatting.

* **Standard Method:** `df.head()` (Shows top 5 rows).
* **Pro Tip:** Use `df.sample(5)` instead.
* **Why?** `head()` might show biased data if the dataset is sorted. `sample()` gives a random snapshot, which is more representative of the overall variety.

### **3. What are the data types of columns?**

Check if the computer interprets the data correctly.

* **Method:** `df.info()`
* **Insight:** * Identifies numerical vs. categorical (object) columns.
* Shows memory usage.
* **Optimization:** You can often reduce memory by converting unnecessary `float64` columns to `int`.



### **4. Are there any missing values?**

Missing data can break your machine learning models.

* **Method:** `df.isnull().sum()`
* **Insight:** This provides a count of null values per column. It helps you decide whether to drop a column (if too many values are missing) or fill them (imputation).

### **5. How does the data look mathematically?**

Understand the distribution and range of numerical values.

* **Method:** `df.describe()`
* **Insight:** Provides mean, standard deviation, min/max, and quartiles (25%, 50%, 75%). This helps identify outliers and the general spread of the data.

### **6. Are there duplicate values?**

Duplicates can lead to overfitting and biased results.

* **Method:** `df.duplicated().sum()`
* **Insight:** Tells you exactly how many rows are identical. These should generally be removed before training.

### **7. How are the columns correlated?**

Identify relationships between different features and the target variable.

* **Method:** `df.corr()` (specifically focusing on the target column).
* **Insight:** Values range from -1 to 1.
* **Positive Correlation:** As one goes up, the other goes up (e.g., higher fare = higher survival chance).
* **Negative Correlation:** As one goes up, the other goes down (e.g., higher class number = lower survival chance)


---

### **Academy Exercise**

**Task:** Load the Titanic dataset (or any local CSV) and write a script that outputs the answers to these 7 questions.
**Goal:** Students should be able to explain *why* they are checking for missing values or correlation before they start coding any graphs.