# Tensors in Machine Learning

## What is a Tensor?

A tensor is a mathematical object that generalizes scalars, vectors, and matrices to higher dimensions. In machine learning, tensors are the fundamental data structure used to represent and manipulate data.

**Simple Definition**: A tensor is an n-dimensional array of numbers with a specific shape and data type.

## Tensor Hierarchy

### 0D Tensor (Scalar)
- A single number
- Shape: `()`
- Example: `5`, `3.14`, `-2`

### 1D Tensor (Vector)
- An array of numbers
- Shape: `(n,)`
- Example: `[1, 2, 3, 4]` has shape `(4,)`

### 2D Tensor (Matrix)
- A 2D array of numbers (rows and columns)
- Shape: `(rows, columns)`
- Example: `[[1, 2], [3, 4], [5, 6]]` has shape `(3, 2)`

### 3D Tensor
- A 3D array of numbers
- Shape: `(depth, rows, columns)`
- Common in image processing (height, width, channels)

### 4D+ Tensors
- Higher dimensional arrays
- Common in deep learning for batches of data

## Key Tensor Properties

### Shape
The dimensions of the tensor
```python
# Example shapes
scalar: ()
vector: (5,)
matrix: (3, 4)
3D tensor: (2, 3, 4)
4D tensor: (10, 28, 28, 3)  # batch_size, height, width, channels
```

### Rank (Number of Dimensions)
- Scalar: rank 0
- Vector: rank 1
- Matrix: rank 2
- 3D tensor: rank 3

### Data Type
- `float32`, `float64`, `int32`, `bool`, etc.
- Affects memory usage and computation precision

## Tensors in Different ML Contexts

### Computer Vision
- **Grayscale Image**: 2D tensor `(height, width)`
- **Color Image**: 3D tensor `(height, width, channels)`
- **Batch of Images**: 4D tensor `(batch_size, height, width, channels)`

### Natural Language Processing
- **Word Embeddings**: 2D tensor `(vocabulary_size, embedding_dim)`
- **Sentence**: 1D tensor `(sequence_length,)` of token IDs
- **Batch of Sentences**: 2D tensor `(batch_size, sequence_length)`

### Time Series
- **Single Series**: 1D tensor `(time_steps,)`
- **Multivariate Series**: 2D tensor `(time_steps, features)`
- **Batch of Series**: 3D tensor `(batch_size, time_steps, features)`

## Common Tensor Operations

### Reshaping
Changing the shape while keeping the same data
```python
# Reshape (6,) to (2, 3)
[1, 2, 3, 4, 5, 6] → [[1, 2, 3], [4, 5, 6]]
```

### Slicing and Indexing
Extracting subsets of data
```python
tensor[0]        # First element/row
tensor[:, 1]     # All rows, second column
tensor[1:3, :]   # Rows 1-2, all columns
```

### Broadcasting
Performing operations on tensors with different shapes
```python
# (3, 1) + (3,) → (3, 3)
[[1], [2], [3]] + [10, 20, 30] → [[11, 21, 31], [12, 22, 32], [13, 23, 33]]
```

### Reduction Operations
- `sum()`, `mean()`, `max()`, `min()`
- Can be applied along specific axes

## Tensor Libraries

### NumPy
```python
import numpy as np
tensor = np.array([[1, 2], [3, 4]])
print(tensor.shape)  # (2, 2)
```

### TensorFlow
```python
import tensorflow as tf
tensor = tf.constant([[1, 2], [3, 4]])
print(tensor.shape)  # (2, 2)
```

### PyTorch
```python
import torch
tensor = torch.tensor([[1, 2], [3, 4]])
print(tensor.shape)  # torch.Size([2, 2])
```

## Why Tensors Matter in ML

### Efficient Computation
- Vectorized operations are much faster than loops
- GPU acceleration works well with tensor operations
- Parallel processing of multiple data points

### Batch Processing
- Process multiple examples simultaneously
- Essential for training neural networks efficiently
- Gradient computations across batches

### Automatic Differentiation
- ML frameworks can automatically compute gradients
- Backpropagation relies on tensor operations
- Chain rule applied through computational graphs

## Common Tensor Patterns in ML

### Input Data
```python
# Image classification
X = (batch_size, height, width, channels)

# Text classification
X = (batch_size, sequence_length, embedding_dim)

# Tabular data
X = (batch_size, num_features)
```

### Neural Network Weights
```python
# Dense layer weights
W = (input_dim, output_dim)

# Convolutional layer weights
W = (filter_height, filter_width, input_channels, output_channels)
```

### Gradients
- Same shape as the corresponding parameters
- Used to update weights during training

## Memory Considerations

### Storage Requirements
```python
# float32 tensor of shape (1000, 1000)
# Memory: 1000 × 1000 × 4 bytes = 4 MB
```

### Contiguous Memory
- Tensors stored in contiguous memory blocks
- Enables efficient vectorized operations
- Some operations may require memory reallocation

## Best Practices

### Shape Debugging
Always check tensor shapes when debugging
```python
print(f"Input shape: {X.shape}")
print(f"Weight shape: {W.shape}")
print(f"Output shape: {Y.shape}")
```

### Memory Management
- Use appropriate data types (`float32` vs `float64`)
- Clear unused tensors from memory
- Use gradient checkpointing for large models

### Batch Dimension
- Always consider the batch dimension in your operations
- Use batch-aware operations when possible
- Handle variable batch sizes gracefully

## Summary

Tensors are the backbone of modern machine learning, providing:
- Efficient representation of multi-dimensional data
- Vectorized operations for fast computation
- Automatic differentiation capabilities
- GPU acceleration support
- Batch processing functionality

Understanding tensors is crucial for working effectively with any ML framework and designing efficient neural network architectures.