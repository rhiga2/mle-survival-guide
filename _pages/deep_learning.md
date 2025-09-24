---
title: Deep Learning
author: Ryley Higa
date: 2024-07-09
category: deep-learning
ordering: 030
layout: post
---
# Computational Graphs
Tensors are n-dimensional arrays of numbers. For example, 0-dimensional tensor are scalars, 1-dimensional tensors are vectors, and 2-dimensional tensors are matrices. **Computational graphs** are directed graphs where each node represents **tensor** operations and each edge represents the composition of operations. Deep learning networks are parameterized (and usually large) computational graphs that support two main operations:
1. Forward propagation takes an input tensor $x$ and transforms the input to an output prediction such as the classification of an image or the next word in a sentence.
2. Backpropagation takes feedback from the output prediction and applies feedback to the parameters of 

# Fully-Connected Networks (TODO)

# Convolutional Networks (TODO)

# Non-Functional Performance Optimizations
## Quantization
* Quantization: reduce the precision (bits) of operators and parameters in a network.
* Why?
  * Less memory (especially VRAM usage)
  * Lower precision operations can be faster during inference.
  * Hardware that supports lower precision calculations can be cheaper.
### Quantization Techniques  
* There are three types of quantization techniques:
   * Dynamic quantization: After training, we quantize the weights. Activations are quantized during runtime.
   * Static quantization: After training, we quantize both the weights and activations.
   * Quantized aware training: During training, we quantize or pseudo-quantize the network in the forward pass.   
## Distillation
* Distillation is a technique for having one model (student) train based on the outputs of another model (teacher).
* Why?
   * Student models may be compressed, less resource-demanding versions of the teacher model.
   * Teacher may be closed source, whereas student may be open source.
### Distillation Techniques
* Use softmax output as training. In this case, it's common to adjudst the softmax output with increased tempurature (softens the distribution) and use KL divergence loss.
*      



