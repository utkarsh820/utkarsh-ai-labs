### **Bivariate & Multivariate Analysis (Finding Connections)**

#### **Objective**

To teach students how to analyze two or more variables simultaneously to discover relationships, correlations, and how features interact with the target variable.

---

### **1. What is Bivariate Analysis?**

"Bi" means two. Bivariate analysis looks at two columns at the same time to see if there is a mathematical or visual relationship between them. This is how we begin to understand _why_ things happen (e.g., does Age affect Survival? Does Square Footage affect House Price?).

We face three scenarios when comparing two variables:

---

### **2. Scenario A: Numerical vs. Numerical**

Comparing two numbers (e.g., Age vs. Fare).

#### **A. Scatterplots**

Scatter plots graph one number on the X-axis and one on the Y-axis.

- **Method:** `sns.scatterplot(x='Age', y='Fare', data=df)`
- **Insight:** Looks for trends. Do the dots form a line going up? That's a positive correlation. Going down? Negative correlation. Random cloud? No correlation.

#### **B. Correlation Matrix & Heatmap**

A mathematical calculation of the linear relationship between all numbers.

- **Method:**
  ```python
  numeric_df = df.select_dtypes(include=['number'])
  sns.heatmap(numeric_df.corr(), annot=True, cmap='coolwarm')
  ```
- **Insight:** Shows exact correlation numbers (-1 to 1) for all numerical columns at once. Deep red/warm means strong positive correlation; deep blue/cool means strong negative correlation.

---

### **3. Scenario B: Categorical vs. Numerical**

Comparing a text label with a number (e.g., Gender vs. Age or Class vs. Fare).

#### **A. Boxplots Grouped by Category**

Shows numerical distributions broken down by category.

- **Method:** `sns.boxplot(x='Pclass', y='Fare', data=df)`
- **Insight:** You can immediately see how the median and outliers of a numerical value change across different categories.

#### **B. Barplots (Mean values)**

Shows the average of the numerical variable for each category.

- **Method:** `sns.barplot(x='Sex', y='Survived', data=df)`
- **Insight:** Automatically calculates the mean (average). In the Titanic dataset, this visually proves that females had a significantly higher survival rate.

---

### **4. Scenario C: Categorical vs. Categorical**

Comparing two text labels (e.g., Gender vs. Survived).

#### **A. Cross-Tabulation (Crosstab)**

Creates a matrix showing the frequency counts of the two categories intersecting.

- **Method:** `pd.crosstab(df['Sex'], df['Survived'])`
- **Insight:** Gives exact numbers. "How many men survived vs died?"

#### **B. Stacked Bar Charts**

A visual representation of the crosstab.

- **Method:** `pd.crosstab(df['Pclass'], df['Survived']).plot(kind='bar', stacked=True)`
- **Insight:** Quickly shows the proportion of survival across different passenger classes.

---

### **Academy Exercise**

**Task:** Load the Titanic dataset (or any local CSV).

1. Create a `heatmap` of the correlations. Which single numerical column has the highest correlation with `Survived`?
2. Create a `boxplot` comparing `Pclass` (Categorical) with `Age` (Numerical). Are 1st class passengers generally older than 3rd class passengers?
