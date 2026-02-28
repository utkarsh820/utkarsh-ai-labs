# Python
# AI/ML Python Stack Mastery Index (0 → Elite)

### 1. Core Python Programming
| Topic Area | Beginner (Foundations) | Intermediate (Engineering) | Advanced / Elite (Optimization & Internals) |
| :--- | :--- | :--- | :--- |
| **Syntax & Data** | Variables, Primitive Types, Type Conversion | Type Hinting (`typing`), Data Classes (`dataclasses`) | Metaclasses, Descriptors, `__slots__` for memory |
| **Control Flow** | If/Else, For/While Loops | List/Dict Comprehensions, `zip`, `enumerate` | Generators (`yield`), Coroutines (`async/await`) |
| **Functions** | Definition, Arguments, Return values | `*args`, `**kwargs`, Lambda, Map/Filter | Decorators (with args), Closures, Functools |
| **Object Oriented** | Classes, Objects, Basic Methods | Inheritance, Polymorphism, Magic Methods (`__init__`) | Abstract Base Classes, Metaprogramming, Mixins |
| **Modules & Env** | Import, Pip install, Basic Scripts | Virtual Environments (`venv`, `poetry`), Package structure | Relative imports, Namespace packages, Wheel building |
| **File I/O** | Read/Write TXT, CSV, JSON | Context Managers (`with`), Pathlib | Memory Mapping (`mmap`), Binary protocols, Pickle safety |
| **Error Handling** | Try/Except, Basic Errors | Custom Exceptions, Logging module | Context propagation, Debugging profilers (`cProfile`) |
| **Concurrency** | Single-threaded scripts | `threading` (I/O), `subprocess` | `multiprocessing` (CPU), GIL bypass, AsyncIO loops |
| **Performance** | Writing working code | Vectorization awareness, Algorithmic complexity | C-Extensions (`PyBind11`), JIT (`Numba`), Memory profiling |

### 2. NumPy (Numerical Computing)
| Topic Area | Beginner (Foundations) | Intermediate (Engineering) | Advanced / Elite (Optimization & Internals) |
| :--- | :--- | :--- | :--- |
| **Arrays** | `np.array`, `np.zeros`, `np.ones` | `np.arange`, `np.linspace`, Data types (`dtype`) | Structured arrays, Record arrays, Memory views |
| **Manipulation** | `reshape`, `flatten`, `transpose` | `concatenate`, `stack`, `squeeze`, `expand_dims` | `stride_tricks`, `as_strided`, In-place operations |
| **Indexing** | Basic slicing `[0:5]` | Boolean masking, Fancy indexing | `np.take`, `np.put`, Advanced stride manipulation |
| **Math Ops** | +, -, *, /, `np.sum`, `np.mean` | `np.dot`, `np.matmul`, Aggregations (`axis`) | `np.einsum`, Universal Functions (UFuncs), Broadcasting rules |
| **Linear Algebra** | `np.linalg.inv`, `np.linalg.det` | Eigenvalues, SVD, Matrix Decomposition | Sparse matrices (`scipy.sparse`), BLAS/LAPACK binding |
| **Random** | `np.random.rand`, `np.random.randint` | `np.random.normal`, Seeds, Distributions | `np.random.Generator`, PCG64, Parallel RNG |
| **Performance** | Python loops over arrays | Vectorization (avoiding loops) | Memory layout (C vs Fortran order), Cache locality |
| **Interoperability** | List to Array conversion | Array to List, Pandas interop | ctypes, C-API, Sharing memory with PyTorch/TensorFlow |

### 3. Pandas (Data Manipulation)
| Topic Area | Beginner (Foundations) | Intermediate (Engineering) | Advanced / Elite (Optimization & Internals) |
| :--- | :--- | :--- | :--- |
| **Structures** | `Series`, `DataFrame` creation | Index management, Column selection | MultiIndex (Hierarchical), Categorical dtype |
| **I/O** | `read_csv`, `to_csv`, `read_excel` | `read_sql`, `to_parquet`, Chunking (`chunksize`) | Feather/Arrow format, Database connectors, S3 integration |
| **Cleaning** | `dropna`, `fillna`, `drop_duplicates` | `replace`, `astype`, String methods (`str.`) | Regex extraction, Custom NA handling, Memory reduction |
| **Selection** | `loc`, `iloc`, Boolean filtering | `query`, `select_dtypes`, `isin` | Index alignment, Reindexing, MultiIndex slicing |
| **Transformation** | `apply`, `map`, `applymap` | Vectorized operations, `assign` | Custom Accessors, `pipe`, GroupBy transformations |
| **Aggregation** | `sum`, `mean`, `count` | `groupby`, `agg`, `pivot_table` | `groupby` internals, Rolling/Expanding windows, Resampling |
| **Merging** | `concat`, `merge` (join) | `join`, `combine_first`, Append | Database-style joins, Overlapping columns, Validation |
| **Time Series** | `to_datetime`, Basic indexing | Date ranges, Frequency conversion, Timezones | Business days, Custom offsets, Lag/Lead features |
| **Performance** | Default dtypes | Downcasting numerics, Categoricals | `eval`/`query` engine, Swapping to Polars, Memory profiling |

### 4. Scikit-Learn (Machine Learning)
| Topic Area | Beginner (Foundations) | Intermediate (Engineering) | Advanced / Elite (Optimization & Internals) |
| :--- | :--- | :--- | :--- |
| **API Standard** | `fit`, `predict`, `score` | `fit_transform`, `inverse_transform` | Custom Estimators, Transformers, Meta-estimators |
| **Preprocessing** | `StandardScaler`, `MinMaxScaler` | `OneHotEncoder`, `Imputer`, `Pipeline` | Custom Transformers, FeatureUnion, ColumnTransformer |
| **Models** | Linear/Logistic Regression, KNN | Decision Trees, Random Forest, SVM | Gradient Boosting (HistGradientBoosting), Ensemble voting |
| **Validation** | `train_test_split` | `cross_val_score`, K-Fold, Stratified K-Fold | TimeSeriesSplit, GroupKFold, Nested CV, Leakage prevention |
| **Metrics** | `accuracy_score`, `mean_squared_error` | Precision/Recall, F1, ROC/AUC, Confusion Matrix | Custom scorers, Multi-output metrics, Probability calibration |
| **Tuning** | Manual parameter change | `GridSearchCV`, `RandomizedSearchCV` | `HalvingGridSearch`, Bayesian Opt (integration), Early stopping |
| **Pipeline** | Basic sequential steps | Feature selection within pipeline | Parallel pipeline execution, Caching (`memory` param) |
| **Serialization** | `pickle` | `joblib.dump`, `joblib.load` | Model versioning, ONNX conversion, Sparse model storage |
| **Scaling** | Single machine, RAM fit | `partial_fit` (Online learning) | Distributed strategies, Out-of-core learning, Approximate nearest neighbors |
