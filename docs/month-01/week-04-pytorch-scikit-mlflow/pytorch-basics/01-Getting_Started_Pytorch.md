# 🎓 Deep Learning Masterclass: Getting Started with PyTorch

## From a Professor & Industry Practitioner Perspective

---

# 📚 LEVEL 1: INTUITION

## What is PyTorch?

**Think of it like NumPy on Steroids, but for AI:**
If you know NumPy, you know how to manipulate arrays (lists of numbers). PyTorch does the exact same thing but with two massive superpowers:

1. **GPU Acceleration:** It can perform calculations on a Graphics Card (GPU) thousands of times faster than a regular CPU.
2. **Automatic Differentiation (Autograd):** It can automatically calculate calculus derivatives (gradients), which is the secret sauce for training neural networks.

## Why Do We Need It?

**The Problem:** Writing deep learning models from scratch in pure Python/NumPy involves agonizing math (backpropagation), manual memory management, and slow execution.

**The Solution:** PyTorch provides a clean, Pythonic way to build deep neural networks. It handles the terrifying calculus for you.

## The Tensor: The Core Building Block

A **Tensor** is just a fancy word for an n-dimensional array.

- **0-D Tensor:** A single number (Scalar) e.g., `5`
- **1-D Tensor:** A list of numbers (Vector) e.g., `[1, 2, 3]`
- **2-D Tensor:** A table of numbers (Matrix) e.g., `[[1, 2], [3, 4]]`
- **3-D Tensor:** A cube of numbers (e.g., an RGB image with Height x Width x Channels)

---

# 📚 LEVEL 2: DEFINITION (Interview/Academic Ready)

## Key Concepts

| **Concept**       | **Definition**                                                                                                     | **Analogy**                                                                         |
| :---------------- | :----------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------- |
| **Tensor**        | A multi-dimensional matrix containing elements of a single data type. The fundamental data structure in PyTorch.   | A highly optimized spreadsheet of numbers that can be moved to a GPU.               |
| **Autograd**      | PyTorch's automatic differentiation engine that records operations to compute gradients backward.                  | A magical ledger that tracks every math operation so it can easily reverse them.    |
| **nn.Module**     | The base class for all neural network modules. Models are structured as subclasses of `nn.Module`.                 | The blueprint/chassis of a car; it holds the engine and parts together.             |
| **Optimizer**     | An algorithm (like SGD or Adam) that updates the model's weights based on the computed gradients to minimize loss. | The steering wheel adjusting the car's direction based on the map (loss landscape). |
| **Loss Function** | A function that computes the difference between the model's prediction and the actual target.                      | The GPS telling you how far off you are from your destination.                      |

---

# 📚 LEVEL 3: TENSORS & OPERATIONS

## 3.1 Creating Tensors

```python
import torch

# From a Python list
x = torch.tensor([1, 2, 3])

# Filled with zeros or ones
zeros = torch.zeros(2, 3)  # 2 rows, 3 columns
ones = torch.ones(2, 3)

# Random numbers
rand_tensor = torch.rand(2, 3)  # Uniform distribution [0,1)
randn_tensor = torch.randn(2, 3) # Normal distribution (mean 0, variance 1)

# Sequence of numbers
seq = torch.arange(0, 10, step=2) # tensor([0, 2, 4, 6, 8])
```

## 3.2 Tensor Attributes

Every tensor has three essential attributes you must know:

1. `shape` / `size()`: The dimensions of the tensor.
2. `dtype`: The data type (e.g., `torch.float32`, `torch.int64`).
3. `device`: Where the tensor lives (`cpu` or `cuda` for GPU).

```python
x = torch.rand(3, 4)
print(f"Shape: {x.shape}")     # torch.Size([3, 4])
print(f"Data type: {x.dtype}") # torch.float32
print(f"Device: {x.device}")   # cpu
```

## 3.3 The Power of the GPU

If a GPU is available, you can dramatically speed up computations by moving tensors to it.

```python
# Check if a GPU is available
device = "cuda" if torch.cuda.is_available() else "cpu"

# Create a tensor directly on the device
x_gpu = torch.rand(3, 3, device=device)

# Or move an existing tensor to the device
x_cpu = torch.rand(3, 3)
x_gpu_moved = x_cpu.to(device)
```

## 3.4 Tensor Operations

PyTorch operations look almost exactly like NumPy.

```python
a = torch.tensor([1, 2])
b = torch.tensor([3, 4])

# Addition
c = a + b              # tensor([4, 6])
c = torch.add(a, b)    # Same thing

# Element-wise multiplication
d = a * b              # tensor([3, 8])

# Matrix Multiplication (Dot Product)
# Note: Dimensions must align! (e.g., (2,3) @ (3,2) -> (2,2))
mat1 = torch.rand(2, 3)
mat2 = torch.rand(3, 2)
result = torch.matmul(mat1, mat2) # OR mat1 @ mat2
```

## 3.5 Shape Manipulation (Crucial for Deep Learning)

Changing the shape of tensors is the most common debugging task in PyTorch.

```python
x = torch.arange(12)  # 1D tensor of 12 numbers

# View / Reshape (changing dimensions)
y = x.view(3, 4)      # Reshape to 3x4 matrix
z = x.reshape(3, 4)   # Safer alternative if memory is non-contiguous

# Squeeze / Unsqueeze (adding/removing dummy dimensions)
x = torch.rand(1, 28, 28) # e.g., 1 image, 28x28 pixels
y = x.squeeze()           # Removes the '1' dimension -> shape [28, 28]

z = y.unsqueeze(dim=0)    # Adds a '1' dimension at index 0 -> shape [1, 28, 28]
```

---

# 📚 LEVEL 4: EXAMPLES WITH CODE & THEORY

## 4.1 The Magic of Autograd (Automatic Differentiation)

This is why PyTorch exists. Let's calculate the gradient of $y = 3x^2 + 2x$ at $x = 2$.
Calculus tells us $\frac{dy}{dx} = 6x + 2$. At $x=2$, the gradient is $14$.

```python
import torch

# 1. Create a tensor and tell PyTorch: "Track everything that happens to this"
x = torch.tensor(2.0, requires_grad=True)

# 2. Perform operations (Forward pass)
y = 3 * x**2 + 2 * x

# 3. Calculate gradients automatically (Backward pass)
y.backward()

# 4. View the gradient (dy/dx)
print(f"Gradient dy/dx at x=2 is: {x.grad}")
# Output: tensor(14.)
```

## 4.2 Building a Simple Neural Network

Let's build a tiny network using `torch.nn`.

```python
import torch
from torch import nn

# Define the model architecture
class SimpleNetwork(nn.Module):
    def __init__(self):
        super().__init__()
        # Define the layers
        self.layer1 = nn.Linear(in_features=10, out_features=5)
        self.activation = nn.ReLU()
        self.layer2 = nn.Linear(in_features=5, out_features=1)

    def forward(self, x):
        # Define the forward computation
        x = self.layer1(x)
        x = self.activation(x)
        x = self.layer2(x)
        return x

# Instantiate the model
model = SimpleNetwork()

# Create dummy data (Batch Size=32, Input Features=10)
dummy_input = torch.randn(32, 10)

# Pass data through the model
predictions = model(dummy_input)

print(f"Input shape: {dummy_input.shape}")
print(f"Output shape: {predictions.shape}") # Should be [32, 1]
```

---

# 📚 LEVEL 5: INDUSTRY INSIGHTS & BEST PRACTICES

## 5.1 PyTorch vs TensorFlow

**Why did PyTorch win the research/industry battle?**

- **Pythonic:** PyTorch feels like writing normal Python.
- **Dynamic Computation Graph:** PyTorch builds the neural network dynamically as the code runs. If you want to use an `if` statement or a `while` loop inside your neural network, you just write normal python code.
- **Debugging:** Because it's dynamic, you can use a normal python debugger (`pdb`) or print statements inside your forward pass.

## 5.2 Top 5 Common Beginner Mistakes

1. **Device Mismatch:** `RuntimeError: Expected all tensors to be on the same device...`
   - _Fix:_ Ensure your model and your data are BOTH on the `cuda` device.
2. **Shape Mismatch:** `RuntimeError: mat1 and mat2 shapes cannot be multiplied...`
   - _Fix:_ Double-check your `nn.Linear` input/output dimensions. Print `x.shape` in your forward pass.
3. **Forgetting to Zero Gradients:** `optimizer.zero_grad()`
   - _Fix:_ PyTorch _accumulates_ gradients by default. You MUST clear them before every new training step, otherwise, the gradients will compound and the math will explode.
4. **Using `.view()` instead of `.reshape()`:**
   - _Fix:_ Use `.reshape()`. `.view()` requires the sequence of data in memory to be contiguous, which sometimes breaks after transposing tensors.
5. **Moving Data to CPU for NumPy:** PyTorch tensors on GPU cannot be converted to NumPy directly.
   - _Fix:_ Call `.detach().cpu().numpy()` to safely pull predictions back to standard arrays.

## 5.3 The Standard PyTorch Training Loop Template

Memorize this structure. 99% of PyTorch training scripts look exactly like this:

```python
# 1. Setup
model = SimpleNetwork().to(device)
criterion = nn.MSELoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)

# 2. Loop over epochs
epochs = 10
for epoch in range(epochs):
    model.train() # Set model to training mode

    # 3. Loop over batches
    for batch_X, batch_y in dataloader:
        batch_X, batch_y = batch_X.to(device), batch_y.to(device)

        # Step A: Forward pass (Predict)
        predictions = model(batch_X)

        # Step B: Calculate Loss
        loss = criterion(predictions, batch_y)

        # Step C: Zero out old gradients
        optimizer.zero_grad()

        # Step D: Calculate new gradients (Backprop)
        loss.backward()

        # Step E: Update weights
        optimizer.step()
```

## 5.4 Best Practices

- Always test your code on a CPU to ensure logic works before launching massive jobs on a GPU cluster.
- Seed everything: `torch.manual_seed(42)` ensures your results are somewhat reproducible while debugging.
- Use `torch.no_grad()` or `torch.inference_mode()` when evaluating models to save memory and speed up inference by disabled gradient tracking.
