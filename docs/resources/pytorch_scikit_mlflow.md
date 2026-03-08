# Resources

# 🎓 Module: PyTorch, Scikit-Learn, & MLflow Resources (0 → Elite)

**Course:** ML Engineering & Deep Learning Frameworks  
**Topic:** Curated Free & Open-Source Resources  
**Cost:** $0 (All Free)

---

## 📘 How to Use This Learning Path

**The Strategy:**

1.  **Start:** Pick **one** resource from "Beginner" to build simple pipelines and neural networks.
2.  **Practice:** Build an end-to-end model with Scikit-Learn, track it in MLflow, or build an image classifier in PyTorch.
3.  **Progress:** Move to "Intermediate" to write custom Datasets and robust machine learning pipelines.
4.  **Master:** Use "Elite" resources to deploy distributed training and write custom CUDA extensions.

---

## 🟢 Level 1: Beginner (0 → 1)

_Goal: Understand the Scikit-Learn API (fit/predict), PyTorch tensors and modules, and basic MLflow logging._

| Resource                      | Type                   | Time    | Why It's Great                                                                    | Link                                                                                                                                   |
| :---------------------------- | :--------------------- | :------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------- |
| **Scikit-Learn User Guide**   | Documentation          | 5 hrs   | Start with the 'Getting Started' page. The most perfectly designed API in Python. | [scikit-learn.org/stable/getting_started.html](https://scikit-learn.org/stable/getting_started.html)                                   |
| **PyTorch 60-Minute Blitz**   | Interactive Docs       | 1-2 hrs | The official entry point to PyTorch. Understand Tensors and Autograd immediately. | [pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html](https://pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html) |
| **MLflow Quickstart**         | Documentation          | 1 hr    | See how 5 lines of code can log your model parameters, metrics, and artifacts.    | [mlflow.org/docs/latest/getting-started/](https://mlflow.org/docs/latest/getting-started/)                                             |
| **PyTorch for Deep Learning** | YouTube (FreeCodeCamp) | 25 hrs  | Daniel Bourke's legendary marathon course. Extremely practical.                   | [youtube.com/watch?v=Z_ikDlimN6A](https://www.youtube.com/watch?v=Z_ikDlimN6A)                                                         |

✅ **Milestone:** You can `fit()` a Scikit-learn model, build a `nn.Sequential` PyTorch model, and view your runs in the MLflow UI.

---

## 🟡 Level 2: Intermediate (1 → 10)

_Goal: Scikit-learn Pipelines/Transformers, PyTorch Custom Datasets/Dataloaders, and the MLflow Model Registry._

| Resource                       | Type                | Time  | Why It's Great                                                                     | Link                                                                                                                         |
| :----------------------------- | :------------------ | :---- | :--------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------- |
| **Scikit-Learn Pipelines**     | Documentation Guide | 3 hrs | Crucial for avoiding data leakage. Learn `Pipeline` and `ColumnTransformer`.       | [scikit-learn.org/stable/modules/compose.html](https://scikit-learn.org/stable/modules/compose.html)                         |
| **PyTorch Lightning Basics**   | Documentation       | 2 hrs | Remove boilerplate PyTorch code and structure large-scale training automatically.  | [lightning.ai/docs/pytorch/stable/](https://lightning.ai/docs/pytorch/stable/)                                               |
| **Writing Custom Datasets**    | PyTorch Docs        | 2 hrs | Move beyond MNIST. Learn `__getitem__` and `__len__` for handling text and images. | [pytorch.org/tutorials/beginner/basics/data_tutorial.html](https://pytorch.org/tutorials/beginner/basics/data_tutorial.html) |
| **MLflow Tracking & Registry** | Tutorials           | 2 hrs | Understand how to transition models from "Staging" to "Production".                | [mlflow.org/docs/latest/model-registry.html](https://mlflow.org/docs/latest/model-registry.html)                             |

✅ **Milestone:** You can write a preprocessing Pipeline, build a PyTorch `Dataset` for your own images, and promote models in MLflow.

---

## 🟣 Level 3: Advanced (10 → 50)

_Goal: Custom loss functions, distributed training, deployment, and optimizing PyTorch graphs._

| Resource                            | Type            | Time   | Why It's Great                                                                      | Link                                                                                                                       |
| :---------------------------------- | :-------------- | :----- | :---------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------- |
| **Full Stack Deep Learning**        | Video Course    | 20 hrs | Focuses on deploying deep learning, MLOps, scaling, and system design.              | [fullstackdeeplearning.com](https://fullstackdeeplearning.com/)                                                            |
| **Distributed Data Parallel (DDP)** | PyTorch Docs    | 5 hrs  | Learn how to train models across multiple GPUs and multiple nodes.                  | [pytorch.org/tutorials/intermediate/ddp_tutorial.html](https://pytorch.org/tutorials/intermediate/ddp_tutorial.html)       |
| **TensorRT & ORT**                  | Docs / Articles | 8 hrs  | Learn how to convert PyTorch models to ONNX to dramatically speed up inference.     | [onnxruntime.ai](https://onnxruntime.ai/)                                                                                  |
| **Serving MLflow Models**           | MLflow Docs     | 3 hrs  | Deploy your MLflow models behind a REST API or package them into Docker containers. | [mlflow.org/docs/latest/models.html#deploy-mlflow-models](https://mlflow.org/docs/latest/models.html#deploy-mlflow-models) |

✅ **Milestone:** You can train a model 4x faster across 4 GPUs and deploy it via a Dockerized REST API.

---

## 🔴 Level 4: Elite (50 → 100)

_Goal: Write custom CUDA kernels, contribute to core frameworks, and build custom MLOps infrastructure._

| Resource                           | Type                | Time    | Why It's Great                                                               | Link                                                                                                           |
| :--------------------------------- | :------------------ | :------ | :--------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------- |
| **Custom C++ and CUDA Extensions** | PyTorch Docs        | 10 hrs  | Write your own highly optimized GPU layers in C++ and expose them to Python. | [pytorch.org/tutorials/advanced/cpp_extension.html](https://pytorch.org/tutorials/advanced/cpp_extension.html) |
| **CUDA Programming Course**        | University Lectures | 30 hrs  | Learn parallel computing GPU architectures (e.g., UPenn CIS 565).            | [cis565-fall-2022.github.io/](https://cis565-fall-2022.github.io/)                                             |
| **PyTorch Source Code**            | GitHub              | Ongoing | Dive deep into the ATen C++ library that powers PyTorch tensors.             | [github.com/pytorch/pytorch](https://github.com/pytorch/pytorch)                                               |

✅ **Milestone:** You understand CUDA thread configurations, memory latency, and ATen internals.

---

## 💡 Pro Tips for Success

1.  **Embrace Scikit-Learn Pipelines:** Never put a raw Pandas dataframe into `fit()`. Always bundle imputation and scaling into a `Pipeline`.
2.  **Use `.shape` Constantly:** In PyTorch, 90% of your bugs will be tensor shape mismatches. Print out `.shape` at every layer when debugging.
3.  **Log Everything:** Use `mlflow.autolog()` for fast tracking, but explicitly log custom dictionaries and plots to save time during model debugging.
