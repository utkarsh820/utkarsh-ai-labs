# Pipelines & ColumnTransformers (From Zero to Elite)

**Level:** Beginner → Elite  
**Time to Complete:** 60 Minutes (Reading + Practice)

---

## 📘 Part 1: The "Why" of Pipelines

### 1. The Amateur's Trap (Data Leakage)

Imagine you are building a Machine Learning model. Here is the process beginners use:

1. Load data.
2. Impute all missing values using the mean.
3. Scale the entire dataset using `StandardScaler`.
4. Split data into `train` and `test`.

**THIS IS WRONG.** This causes **Data Leakage**. By calculating the mean on the _entire_ dataset in step 2, information from the `test` set "leaked" into the `train` set. Your model got a sneak peek at the test data before evaluating it.

### 2. The Solution

You must:

1. Split data into `train` and `test` FIRST.
2. `fit` the Imputer/Scaler ONLY on the `train` set.
3. `transform` the `train` and `test` sets independently.

This prevents leakage, but the code becomes a tangled, repetitive nightmare of `x_train_scaled = scaler.transform(x_train)`.

A **Pipeline** automates this perfectly.

---

## 🟢 Level 1: The Foundation (`Pipeline`)

**What it is:** A sequence of data transformations ending with a model. It chains everything together.

```python
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

# Define the sequence of steps (List of Tuples: Name, Object)
my_pipeline = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')), # Step 1: Fill missing values
    ('scaler', StandardScaler()),                  # Step 2: Scale data
    ('model', LogisticRegression())                # Step 3: Train model
])

# Training the entire pipeline on training data
my_pipeline.fit(X_train, y_train)

# Predicting on test data (Imputer and Scaler are applied AUTOMATICALLY!)
predictions = my_pipeline.predict(X_test)
```

> **💡 The Golden Rule:** Inside a Pipeline, every step except the last one must have a `.transform()` method. The last step only needs a `.predict()` method.

---

## 🟡 Level 2: The Parallel Split (`ColumnTransformer`)

Pipelines execute sequentially (one after another). But what if your dataset has both Numbers (Age, Salary) and Categories (Gender, City)? You can't put text into a `StandardScaler`.

**What it is:** A `ColumnTransformer` allows you to split the data into parallel paths, apply different transformations to each path, and then seamlessly stitch them back together.

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder

# Define the lists of columns you want to target
numeric_features = ['Age', 'Salary']
categorical_features = ['Gender', 'City']

# Define the parallel paths (Tuples: Name, Transformer, Columns)
preprocessor = ColumnTransformer(transformers=[
    ('num', StandardScaler(), numeric_features),
    ('cat', OneHotEncoder(drop='first'), categorical_features)
])

# This runs in parallel, then concatenates the results horizontally.
processed_data = preprocessor.fit_transform(X_train)
```

---

## 🟠 Level 3: The Master Architecture (Combining Both)

Real-world Machine Learning requires putting Pipelines _inside_ ColumnTransformers, and putting ColumnTransformers _inside_ a Master Pipeline. It looks like this:

```python
from sklearn.ensemble import RandomForestClassifier

# 1. Numeric Path
numeric_pipeline = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

# 2. Categorical Path
categorical_pipeline = Pipeline([
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('encoder', OneHotEncoder(handle_unknown='ignore'))
])

# 3. The Junction (ColumnTransformer)
preprocessor = ColumnTransformer([
    ('num', numeric_pipeline, numeric_features),
    ('cat', categorical_pipeline, categorical_features)
])

# 4. The Master Final Pipeline
master_pipe = Pipeline([
    ('preprocessing', preprocessor),
    ('classifier', RandomForestClassifier())
])

# Just one line of code trains the ENTIRE architecture!
master_pipe.fit(X_train, y_train)
```

---

## 🟣 Level 4: Elite Workflows

### 1. Visualizing the Architecture

If you want to look like a senior engineer, turn on Scikit-Learn's interactive HTML diagram feature. In a Jupyter Notebook:

```python
from sklearn import set_config
set_config(display='diagram')

# Now just type your pipeline name and it renders a beautiful flowchart!
master_pipe
```

### 2. Accessing Inner Steps

Sometimes you need to pull out a specific piece of the pipeline (like checking Feature Importance). You use `.named_steps`.

```python
# Access the random forest model trained at the end of the pipeline
rf_model = master_pipe.named_steps['classifier']
importances = rf_model.feature_importances_
```

### 3. Hyperparameter Tuning across the entire pipeline

You can use GridSearch to tune not just your model, but your preprocessing steps simultaneously (e.g., Should the Imputer use 'mean' or 'median'?). Use the double-underscore `__` syntax.

```python
from sklearn.model_selection import GridSearchCV

# Syntax: step_name__parameter_name
param_grid = {
    'preprocessing__num__imputer__strategy': ['mean', 'median'],
    'classifier__n_estimators': [100, 200]
}

grid = GridSearchCV(master_pipe, param_grid, cv=5)
grid.fit(X_train, y_train)
```

---

## 🏁 Academy Exercise

**Task:**

1. Load the Titanic Dataset.
2. Define numeric features (`Age`, `Fare`) and categorical features (`Sex`, `Embarked`).
3. Build a `ColumnTransformer` that imputes missing values and applies the correct scaling/encoding to each.
4. Chain this preprocessor into a `Pipeline` containing a `LogisticRegression` model.
5. Print the score of the pipeline using `cross_val_score(master_pipe, X, y, cv=5)`.
