# Introduction to CNNs (Convolutional Neural Networks)

## Overview
Convolutional Neural Networks (CNNs) are a specialized type of artificial neural network designed specifically for processing structured grid data, such as images. Unlike traditional fully connected networks that flatten multi-dimensional data, CNNs preserve the spatial relationships between pixels, making them incredibly powerful for computer vision tasks like image classification, object detection, and facial recognition.

---

## 🚀 Beginner Level: The Basics
**What is a CNN?**
Imagine you want to teach a computer to recognize a dog in a photo. A standard neural network would look at every single pixel individually, losing the context of shapes like ears or paws. A CNN, on the other hand, scans the image in small chunks (like looking through a magnifying glass) to detect edges, curves, and patterns. 

**Why use CNNs over regular Neural Networks?**
- **Spatial Awareness:** CNNs understand that a pixel is related to its neighbors.
- **Parameter Sharing:** Instead of learning separate weights for every pixel, CNNs use the same "filter" across the entire image, drastically reducing the number of learned parameters.
- **Translation Invariance:** A CNN can recognize an object regardless of where it appears in the image (e.g., a dog in the top-left corner vs. the bottom-right).

---

## 🧠 Intermediate Level: How Do They Differ?
In a standard purely dense network (Multilayer Perceptron), each neuron in a layer connects to all neurons in the previous layer. For an image of size $224 \times 224 \times 3$, a single neuron in the first hidden layer would need over 150,000 weights!

CNNs solve this using two key concepts:
1. **Local Connectivity:** Neurons are only connected to a small spatial region of the input volume (a receptive field).
2. **Convolution Operation:** Instead of simple matrix multiplication, CNNs apply mathematical convolutions using learnable kernels (filters) that slide (convolve) across the image to produce feature maps.

These structural differences allow CNNs to learn a hierarchy of features:
- **Early layers:** Detect low-level features like edges, lines, and colors.
- **Middle layers:** Combine edges to detect shapes, corners, and textures.
- **Deep layers:** Combine shapes to recognize high-level objects like faces, cars, or dogs.

---

## 🔬 Advanced Level: Mathematical Foundation of Convolutions
The core of a CNN is the convolution operation. For a 2D image $I$ and a 2D filter (kernel) $K$, the convolution is mathematically defined as:

$$ (I * K)(i, j) = \sum_m \sum_n I(i+m, j+n) K(m, n) $$

**Key hyper-parameters affecting the convolution:**
- **Kernel Size ($F$):** The spatial dimensions of the filter (often $3 \times 3$ or $5 \times 5$).
- **Stride ($S$):** The step size with which the filter slides across the image. A stride of 2 halves the output spatial dimensions.
- **Padding ($P$):** Adding zeros around the boundary of the input image to preserve spatial dimensions after convolution (e.g., "Same" padding).

The output size of a convolutional layer given an input volume of size $W$, filter size $F$, stride $S$, and padding $P$ is calculated as:
$$ Output = \frac{W - F + 2P}{S} + 1 $$

---

## 💻 Code Implementation (PyTorch)
Here is how you define a basic CNN block in PyTorch:

```python
import torch
import torch.nn as nn

class BasicCNNBlock(nn.Module):
    def __init__(self, in_channels, out_channels):
        super(BasicCNNBlock, self).__init__()
        # Convolutional layer
        self.conv = nn.Conv2d(
            in_channels=in_channels, 
            out_channels=out_channels, 
            kernel_size=3, 
            stride=1, 
            padding=1 # Same padding
        )
        self.relu = nn.ReLU()
        self.pool = nn.MaxPool2d(kernel_size=2, stride=2)
        
    def forward(self, x):
        x = self.conv(x)
        x = self.relu(x)
        x = self.pool(x)
        return x

# Example usage:
# Input tensor shape: (Batch Size, Channels, Height, Width)
dummy_input = torch.randn(1, 3, 64, 64) 
model = BasicCNNBlock(in_channels=3, out_channels=16)
output = model(dummy_input)

print(f"Input shape: {dummy_input.shape}")
print(f"Output shape: {output.shape}") # Expect (1, 16, 32, 32)
```

---

## 💼 Interview Questions & Answers

**Q1: What is the main advantage of weight sharing in CNNs?**
**A:** Weight sharing drastically reduces the number of learnable parameters in the network compared to fully connected layers, preventing overfitting and making the model computationally efficient. It also allows the network to detect a specific feature anywhere in the image (translation invariance).

**Q2: How does a CNN handle color images compared to grayscale images?**
**A:** A grayscale image has 1 color channel (depth=1), while a color image typically has 3 channels (RGB, depth=3). In a CNN, the filters inherently have a depth matching the input volume. For an RGB image, a $3 \times 3$ filter is actually $3 \times 3 \times 3$ (width $\times$ height $\times$ channels). The convolution operation sums across all channels to produce a single 2D feature map per filter.
