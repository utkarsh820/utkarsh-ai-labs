### **Univariate Analysis (One Variable at a Time)**

#### **Objective**

To teach students how to examine single variables in isolation to understand their distribution, central tendency, and identify potential outliers before comparing them with other variables.

---

### **1. What is Univariate Analysis?**

**Univariate Data Analysis** is the simplest form of data analysis. "Uni" means one, so in other words, you are looking at one specific column (variable) of your dataset at a time. The purpose is to describe the data and find patterns that exist within it.

There are two main types of data we analyze this way:

1. **Numerical Data** (Continuous or Discrete numbers, e.g., Age, Salary)
2. **Categorical Data** (Text labels or groups, e.g., Gender, City)

---

### **2. Analyzing Numerical Data**

When analyzing numbers, we want to see the "shape" of the data and find extreme values (outliers).

#### **A. Histograms (The Distribution Shape)**

A histogram groups numbers into bins to show where most values fall.

- **Method:** `sns.histplot(df['column_name'], kde=True)`
- **Insight:** Is the data normally distributed (bell curve)? Is it skewed to the left or right?
- **Example:** Most people on the Titanic were between 20 and 30 years old, but the histogram has a long "tail" reaching up to 80.

#### **B. Boxplots (Spotting Outliers)**

A boxplot provides a visual summary of the data's quartiles (25%, 50%, 75%) and explicitly dots out the outliers.

- **Method:** `sns.boxplot(x=df['column_name'])`
- **Insight:** The "box" shows the middle 50% of your data. The "whiskers" show the normal range. Any dots outside the whiskers are mathematical outliers.

---

### **3. Analyzing Categorical Data**

When analyzing text categories, we want to know the frequency (how many times each category occurs).

#### **A. Countplots (The Bar Chart for Categories)**

A countplot automatically counts the occurrences of each category and displays them as bars.

- **Method:** `sns.countplot(x=df['category_column'])`
- **Insight:** You can quickly see which category dominates the dataset.
- **Example:** `sns.countplot(x=df['Survived'])` clearly shows that more people died than survived.

#### **B. Pie Charts (Proportions)**

While less favored by statisticians, pie charts are good for seeing percentage breakdowns.

- **Method:** `df['category_column'].value_counts().plot(kind='pie', autopct='%1.1f%%')`
- **Insight:** Shows what "slice of the pie" each category represents out of 100%.

---

### **Academy Exercise**

**Task:** Load the Titanic dataset (or any local CSV).

1. Create a Histogram for the `Age` column and note its skewness.
2. Create a Boxplot for the `Fare` column. Are there outliers? How extreme are they?
3. Create a Countplot for the `Embarked` column. Which port did most passengers board from?
