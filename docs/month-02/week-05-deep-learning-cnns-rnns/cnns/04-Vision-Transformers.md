# Vision Transformers (ViT)

## Overview
For a decade, Convolutional Neural Networks (CNNs) were the undisputed kings of computer vision. In 2020, researchers at Google Brain introduced the **Vision Transformer (ViT)** in the paper *"An Image is Worth 16x16 Words."* ViT demonstrated that Transformers—originally designed for Natural Language Processing (like BERT and GPT)—could directly process images and achieve state-of-the-art results, fundamentally shifting the computer vision landscape.

Unlike CNNs, which use sliding filters to explicitly look for local patterns (translation invariance), a Vision Transformer treats an image as a sequence of discrete "words" (patches) and uses a self-attention mechanism to learn global relationships between them.

---

## 🚀 Beginner Level: How Does ViT Work?
Think of how you look at a puzzle. A CNN looks at the puzzle piece by piece, checking if the edges fit together locally. A ViT takes all the individual puzzle pieces, scatters them on the table, and instantly compares every piece to every other piece to figure out the whole picture at once.

**The ViT Process:**
1. **Divide into Patches:** The image isn't processed pixel by pixel. It gets chopped up into a grid of non-overlapping squares (e.g., $16 \times 16$ pixel patches).
2. **Flatten & Map (Linear Projection):** Each patch is mathematically flattened into a single 1D vector (an "embedding"). Now, instead of a 2D image, we have a 1D sequence of "image words."
3. **Add Position Information:** Because Transformers process all inputs simultaneously, they have no concept of "left" or "right." We must mathematically tag each patch with its original position (Positional Embedding) so the model knows where the patch came from.
4. **Pass through the Transformer Encoder:** The sequence of patches goes through a standard Transformer architecture (the exact same architecture used in LLMs) utilizing Self-Attention.
5. **Classification Token:** A special dummy patch (the `[CLS]` token) is prepended to the sequence. After passing through the entire network, the model looks *only* at the output state of this token to make its final classification (e.g., "This is a cat").

---

## 🧠 Intermediate Level: Self-Attention vs. Convolutions

### The Problem with Convolutions (CNNs)
Convolutions have an **inductive bias**. They are hard-coded to assume that pixels close to each other are related (locality) and that a pattern in the top-left corner means the same thing if it appears in the bottom-right (translation invariance). 
- **Pro:** This makes CNNs highly data-efficient. They learn very fast on small datasets.
- **Con:** It limits their capacity because they "force" a specific way of seeing the world. To understand a relationship between two far-apart objects in an image, a CNN needs many deep layers to expand its receptive field.

### The Power of Self-Attention (ViTs)
Self-Attention has **no inductive bias regarding images**. It does not inherently know that a patch is a square or that two patches are next to each other.
- It compares *every* patch with *every other* patch in the image simultaneously (Global Receptive Field from layer 1).
- **Pro:** It can learn complex, long-range dependencies across the image much better than a CNN.
- **Con:** Because it lacks the "helpful hints" (inductive biases) of a CNN, a ViT requires **massive amounts of data** (e.g., JFT-300M dataset) to figure out the rules of vision entirely from scratch. On small datasets (like ImageNet from scratch), ViT often performs worse than CNNs!

---

## 🔬 Advanced Level: Mathematical Deep Dive into Self-Attention
In the Transformer Encoder block, the core operation is Multi-Head Self-Attention (MSA).

For an input sequence of patch embeddings $X$, three matrices are computed via linear transformations:
1. **Query ($Q = XW_q$)**
2. **Key ($K = XW_k$)**
3. **Value ($V = XW_v$)**

The attention scores are calculated using scaled dot-product attention:
$$ \text{Attention}(Q, K, V) = \text{softmax} \left( \frac{QK^T}{\sqrt{d_k}} \right) V $$

- **$QK^T$**: This matrix multiplication compares every patch's query against every patch's key. High dot products mean the patches are strongly related.
- **Softmax**: Converts scores into probabilities (attention weights) summing to 1.
- **$V$**: The original patch information is multiplied by the attention weights. If Patch A strongly attends to Patch B, the final representation of Patch A will incorporate a lot of information from Patch B.

This happens simultaneously across multiple "heads," allowing the model to focus on different types of relationships (e.g., one head might look at color similarity, another might associate object parts like wheels to a car chassis).

---

## 💻 Code Implementation: Patch Extraction (PyTorch)
The most unique part of ViT is converting an image into a sequence of patches. Here is a simple demonstration:

```python
import torch
import torch.nn as nn

class PatchEmbedding(nn.Module):
    def __init__(self, img_size=224, patch_size=16, in_channels=3, embed_dim=768):
        super().__init__()
        self.num_patches = (img_size // patch_size) ** 2
        # A Conv2d layer with stride == patch_size perfectly extracts non-overlapping patches
        # and projects them strictly into the `embed_dim` in one step!
        self.proj = nn.Conv2d(
            in_channels, embed_dim, 
            kernel_size=patch_size, stride=patch_size
        )

    def forward(self, x):
        # x shape: (Batch Size, Channels, Height, Width) -> (B, 3, 224, 224)
        x = self.proj(x) 
        # Output shape: (B, embed_dim, grid_h, grid_w) -> (B, 768, 14, 14)
        
        x = x.flatten(2) # Flatten spatial dimensions -> (B, 768, 196)
        x = x.transpose(1, 2) # Swap to sequence format -> (B, 196, 768)
        # Note: 196 is the sequence length (14x14 patches), 768 is the token embedding size
        return x

# Test the patcher
dummy_img = torch.randn(1, 3, 224, 224)
patcher = PatchEmbedding()
patches = patcher(dummy_img)

print(f"Original Image: {dummy_img.shape}")
print(f"Sequence of Patches: {patches.shape}  -> (Batch, Sequence Length, Embedding Dim)")
```

---

## 💼 Interview Questions & Answers

**Q1: Why does a Vision Transformer usually perform worse than a CNN when trained from scratch on a small dataset like ImageNet-1k (1.2M images)?**
**A:** CNNs possess strong inductive biases like translation invariance and local neighborhood connectivity, which act as a powerful regularization prior. ViTs lack these structural biases and must learn everything from the raw data. On smaller datasets, the ViT doesn't have enough examples to deduce these visual rules, leading to overfitting or sub-optimal feature learning. ViTs only surpass CNNs when trained on massive proprietary datasets (like JFT-300M) before being fine-tuned on smaller target datasets.

**Q2: What is the purpose of the `[CLS]` token in a Vision Transformer?**
**A:** Because standard Self-Attention updates the state of every input token independently based on its context, we end up with 196 different patch embeddings at the end of the network. Instead of figuring out how to average or pool them together for classification, we simply insert a learnable placeholder token `[CLS]` at the beginning. By the end of the network, through self-attention layers, this specific token has inherently gathered all the global information necessary from the rest of the image to make an informed classification prediction.
