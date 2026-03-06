### **Feature Engineering & Preprocessing**

#### **Objective**

To teach students how to prepare raw data for machine learning models. Machine learning algorithms only understand numbers. Feature engineering is the art of fixing missing data, turning text into numbers, and helping models learn faster.

---

### **1. Handling Missing Values (Imputation)**

Many models (like Scikit-Learn's Linear Regression) will crash if they encounter `NaN` (blank) values.

- **Option A: Dropping Data**
  - `df.dropna()`: Deletes rows with any missing values. Only do this if very few rows are missing across the entire dataset.
- **Option B: Imputation (Filling)**
  - Fill with **Mean/Median** (for numbers): `df['Age'].fillna(df['Age'].median(), inplace=True)`
  - Fill with **Mode** (for categories): `df['Embarked'].fillna(df['Embarked'].mode()[0], inplace=True)`

---

### **2. Encoding Categorical Data**

Machine learning models cannot read "Male" or "Female"—they require `0` and `1`.

#### **A. Label Encoding (Ordinal Data)**

Use this when categories have a natural order (e.g., Small < Medium < Large).

- **Code Example (Pandas map):**
  ```python
  df['Size'] = df['Size'].map({'Small': 1, 'Medium': 2, 'Large': 3})
  ```
- **Warning:** Do not use Label Encoding for nominal data (like Colors or Cities), because the model will think City #3 is mathematically "greater" than City #1.

#### **B. One-Hot Encoding (Nominal Data)**

Use this when categories have no specific order (e.g., Male/Female, or Cities). It creates a new binary column for every category.

- **Code Example (Pandas get_dummies):**
  ```python
  df = pd.get_dummies(df, columns=['Sex', 'Embarked'], drop_first=True)
  ```
- **Concept:** `drop_first=True` avoids the "Dummy Variable Trap" (perfect collinearity). If `is_female` is 0, the model inherently knows the person is male. You don't need a separate `is_male` column.

---

### **3. Feature Scaling**

Distance-based algorithms (like KNN or SVM) and Gradient Descent algorithms are highly sensitive to the scale of numbers. If 'Age' goes from 0-100 and 'Salary' goes from 0-100,000, the model will treat Salary as 1,000x more important in its distance calculations.

#### **A. Normalization (Min-Max Scaling)**

Squashes all numbers to be exactly between 0 and 1.

- **Best for:** Image processing or Neural Networks that expect inputs $\in [0, 1]$.
- **Method:**
  ```python
  from sklearn.preprocessing import MinMaxScaler
  scaler = MinMaxScaler()
  df[['Age', 'Fare']] = scaler.fit_transform(df[['Age', 'Fare']])
  ```

#### **B. Standardization (Z-score Scaling)**

Centers the data around a mean of 0 with a standard deviation of 1.

- **Best for:** Most modern ML algorithms (Logistic Regression, SVM, PCA). It handles outliers slightly better than Normalization.
- **Method:**
  ```python
  from sklearn.preprocessing import StandardScaler
  scaler = StandardScaler()
  df[['Age', 'Fare']] = scaler.fit_transform(df[['Age', 'Fare']])
  ```

---

### **4. Creating New Features**

Sometimes, the best predictor isn't in your standalone data—it's a combination of your data.

- **Example on Titanic:** Creating a `FamilySize` column by adding `SibSp` (siblings/spouses) and `Parch` (parents/children).
  ```python
  df['FamilySize'] = df['SibSp'] + df['Parch'] + 1
  ```
- **Why?** A model might find that traveling completely alone vs traveling with a family heavily influenced survival rates, a pattern it might struggle to see looking at siblings and parents separately.

---

### **Academy Exercise**

**Task:** Build a rudimentary Preprocessing Pipeline on the Titanic dataset.

1. Fill missing `Age` values with the Median.
2. Fill missing `Embarked` values with the Mode.
3. Apply One-Hot Encoding (`pd.get_dummies`) to `Sex` and `Embarked`.
4. Create a new feature `IsAlone` (1 if `FamilySize == 1`, else 0).
