# 🎓 MLOps Masterclass: Data Version Control (DVC) for Pros

## From a Senior ML Engineer Perspective

---

# 📚 LEVEL 1: INTUITION

## Why Do We Need DVC?

**Think of it as Git for Data and Models:**
You probably use Git for your code. But what happens when you try to use Git for your training datasets (`data.csv` - 5GB) or your saved model weights (`model.pth` - 2GB)?
Git will crash, freeze, or reject your push. GitHub has file size limits for a reason.

**The Problem DVC Solves:**
In Machine Learning, **Code + Data + Hyperparameters = Model**. If you only version your code, you cannot reproduce your model later because the data might have changed.

**The Solution:**
DVC works _alongside_ Git.

- **Git** tracks your code (`train.py`).
- **DVC** tracks your large files (`data.csv`, `model.pth`) and pushes the actual heavy files to cloud storage (S3, GCS, Azure Blob, or a shared drive).
- DVC creates tiny text files (`data.csv.dvc`) holding the **metadata** (a hash of the file). You commit this _tiny text file_ to Git.

Git knows _which_ version of data you used. DVC knows _where_ to find it.

---

# 📚 LEVEL 2: DEFINITION (Interview & Architecture Ready)

## Key Concepts of DVC

| **Concept**                     | **Definition**                                                                                                                                | **Analogy**                                                                  |
| :------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------- |
| **`.dvc` file**                 | A tiny metadata file (e.g., `data.csv.dvc`) that contains a unique hash (MD5) of your large dataset. You commit this to Git.                  | A coat check ticket. Git holds the ticket; DVC holds the actual coat (data). |
| **DVC Cache**                   | A hidden local directory (`.dvc/cache`) where DVC stores the actual large files, renamed by their MD5 hashes.                                 | The backstage storage room where all the actual heavy boxes are kept.        |
| **DVC Remote**                  | The cloud storage (S3, Google Drive, Azure Blob, SSH) where your large files are pushed for the whole team to access.                         | The warehouse where all team members send their heavy boxes.                 |
| **`dvc.yaml`**                  | A configuration file defining your ML pipeline (e.g., extract -> train -> evaluate). It specifies inputs (deps), outputs (outs), and metrics. | The factory assembly line blueprint ensuring everything is built in order.   |
| **DVC Repro (Reproducibility)** | The command (`dvc repro`) that reruns your pipeline _only_ if the underlying data, code, or parameters have changed.                          | A smart compiling system (like `Make`) tailored for Data Science.            |

---

# 📚 LEVEL 3: SETUP & CORE WORKFLOW (The "Hello World" of DVC)

## 3.1 Initializing DVC (Must be done inside a Git repo)

```bash
# First, you must have a git repository
git init

# Then, initialize DVC
dvc init

# DVC creates some internal files. Commit them to Git.
git commit -m "Initialize DVC"
```

## 3.2 Tracking Data (Instead of `git add`, use `dvc add`)

Imagine you have a 10GB file: `data/raw_dataset.csv`.

```bash
# 1. Ask DVC to track the large file
dvc add data/raw_dataset.csv

# What happens under the hood?
# - DVC moves `raw_dataset.csv` into `.dvc/cache/` (hashing it).
# - DVC replaces `raw_dataset.csv` with a symlink/hardlink to the cache.
# - DVC creates `data/raw_dataset.csv.dvc` (a tiny text file).
# - DVC modifies `.gitignore` to ensure Git ignores the real `raw_dataset.csv`.

# 2. Tell Git to track the DVC metadata file and the .gitignore
git add data/raw_dataset.csv.dvc data/.gitignore
git commit -m "Track raw dataset with DVC"
```

## 3.3 Sharing Data (Setting up a Remote)

Like `git remote add origin...`, you need a place for the team to pull data from. Let's use AWS S3 as an example.

```bash
# 1. Add cloud storage as the default DVC remote
dvc remote add -d myremote s3://my-mlops-bucket/dvcstore

# 2. Commit the remote configuration to Git (lives in .dvc/config)
git add .dvc/config
git commit -m "Configure S3 remote for DVC"

# 3. Push the actual large data to S3
dvc push
```

## 3.4 Retrieving Data (The Teammate's Workflow)

When a new engineer joins the team, they run:

```bash
git clone https://github.com/my-org/my-ml-project.git
cd my-ml-project

# The data files are missing! Only the .dvc files are here.
# Download the heavy data files from S3 based on the Git commit:
dvc pull
```

---

# 📚 LEVEL 4: THE PRO USAGE - PIPELINES & REPRODUCIBILITY

Using `dvc add` is nice, but true pros use **DVC Pipelines** (`dvc.yaml`). It explicitly links your code, data, and models together.

Imagine a simple pipeline:

1. `prepare.py`: reads `data/raw.csv` $\rightarrow$ outputs `data/prepared.csv`
2. `train.py`: reads `data/prepared.csv` $\rightarrow$ outputs `model.pkl`

## 4.1 Defining the Pipeline (`dvc.yaml`)

You can create this manually or using `dvc stage add`. Here is the manual `dvc.yaml` file:

```yaml
stages:
  prepare:
    cmd: python src/prepare.py
    deps:
      - src/prepare.py
      - data/raw.csv # If raw.csv changes, rerun this stage
    params:
      - prepare.split_ratio # If this parameter changes in params.yaml, rerun
    outs:
      - data/prepared.csv # DVC automatically tracks this output!

  train:
    cmd: python src/train.py
    deps:
      - src/train.py
      - data/prepared.csv
    params:
      - train.learning_rate
      - train.estimators
    outs:
      - models/model.pkl # DVC tracks the model
    metrics:
      - metrics.json:
          cache: false # Just a lightweight JSON file
```

## 4.2 Run the Pipeline

```bash
params.yaml</code> file
#   - It checks the MD5 hashes of all `deps`.
#   - If nothing changed, it says "Stage 'train' didn't change, skipping."
#   - If data/raw.csv changed, it runs 'prepare', then 'train'.
```

## 4.3 Experiment Tracking (DVC Metrics & Params)

If you modify `params.yaml` (changing learning rate from 0.01 to 0.05) and run `dvc repro`, DVC tracks these experiments.

```bash
# Show all metrics across different Git branches/commits!
dvc metrics show

# Compare metrics across experiments
dvc params diff
dvc metrics diff
```

---

# 📚 LEVEL 5: INDUSTRY BEST PRACTICES & MLOPS INTEGRATION

## 5.1 DVC vs. MLflow: Do I need both?

**YES, they complement each other perfectly.**

- **DVC** is the foundation: It versions your massive datasets, handles cloud storage sync, and defines the rigid, reproducible execution graph (pipeline).
- **MLflow** is the dashboard: It logs hundreds of fast, iterative experiments (accuracy, charts, tensorboard).

**The Pro Workflow:**
Use DVC to construct the DAG (`dvc repro`). Inside your Python scripts (`train.py`), use `mlflow.log_params()` and `mlflow.log_metrics()` to visualize the training curves.

## 5.2 Optimizing Large Data Sync (Hardlinks & Symlinks)

By default, when you run `dvc pull`, DVC _copies_ the file from `.dvc/cache` to your workspace. If you have a 50GB dataset, you now use 100GB of disk space.

**Pro Tip:** Configure DVC to use file links to save massive disk space.

```bash
# Tell DVC to use symlinks (or hardlinks on Windows) instead of copying
dvc config cache.type symlink,hardlink,copy
dvc checkout --relink
```

## 5.3 CI/CD Integration with DVC (CML - Continuous Machine Learning)

You can run your models automatically in GitHub Actions by installing DVC. Iterative (the company behind DVC) provides **CML**.

**Example GitHub Action (`.github/workflows/train.yml`):**

```yaml
name: Train model on Pull Request
on: [pull_request]

jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: iterative/setup-cml@v1
      - uses: iterative/setup-dvc@v1

      - name: Train model
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        run: |
          # Pull data from S3
          dvc pull

          # Reproduce the pipeline
          dvc repro

          # Generate a markdown report and post it as a PR comment
          git fetch --prune
          dvc metrics diff --show-md main > report.md
          cml comment create report.md
```

## 5.4 Handling Multiple Environments (Dev/Staging/Prod)

You often don't want everyone pushing to the production S3 bucket.

```bash
# Add a remote for dev
dvc remote add -d dev_remote s3://my-bucket/dev
# Add a remote for prod
dvc remote add prod_remote s3://my-bucket/prod

# Push experimental data to dev
dvc push

# When the model is approved, push specifically to prod
dvc push -r prod_remote
```

## 5.5 Avoid `dvc push` on tiny text files

Do NOT `dvc add` your `code.py` or small JSON config files. Let Git handle text and code. DVC should strictly handle binaries, large CSVs, images, embeddings, and model `.pkl`/`.pth` artifacts (usually files > 10MB).

> **A Pro Reminder:** Treat your data and models as an extension of your codebase. If you checkout `git checkout v1.0`, your codebase goes back in time. You immediately type `dvc checkout`, and your data and model weights perfectly align with that v1.0 point in time. That is the magic of MLOps.
