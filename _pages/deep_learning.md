---
title: Deep Learning
author: Ryley Higa
date: 2024-07-09
category: deep-learning
ordering: 030
layout: post
---
# Computational Graphs
* Common way to represent deep networks. 
* Tensors are an n-dimensional array of numbers.
* Computational graphs are directed graphs that represents composition of operations on tensors.
* Each node represents a tensor operation and each edge represents the flow of tensors from one operator to another (composition).

## Forward and Backward Propagation
* Forward propagation: given input and parameter tensors to the graph compute the final output.
* Backward propagation: given feedback signal computed on the graph's output, compute feedback on the input and parameter tensors.

# Fully-Connected Networks (TODO)

# Convolutional Networks (TODO)

# Transformers
## Attention Mechanism
### Scaled Dot-Product Attention
* We are given input queries $Q$, keys $K$, and values $V$. Let $d$ be the number of columns in $K$. 
* We calculate the scaled dot product attention as follows.

$$
\begin{gathered}
Y = \text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d}}\right) V
\end{gathered}
$$

### Self-Attention
* Self-attention refers to attention where the queries, keys, and values are all from the same input sequence. As opposed to cross attention where the queries can come from a different input sequence as the keys and values.
* We do this by applying weight matrices to the input $X$.

$$
\begin{gathered}
Q = W^Q X \\
V = W^V X \\
K = W^K X \\
\end{gathered}
$$

### Multi-Head Attention (MHA)
* Sometimes attention depends on different aspects of the input sequence. To capture this intuition, we want to give attention layers different representations of the input sequence $X$.
* We calculate multiple queries, keys, and values by applying different weight matrices $W^Q_i$, $W^K_i$, and $W^V_i$ respectively on the input where $i$ is the index of the head. 
* We then concatenate the outputs of each head and apply a final weight matrix $W^O$ to get the final output.

### Masked Attention
* Sometimes we don't want to give any attention to a future token in the sequence, meaning a query should not retrieve a future key-value pair.
* To do this we zero out the upper triangular portion of the attention matrix before applying the softmax.

$$
\begin{gathered}
M_{ij} = \begin{cases}
   1  & i < j \\
   -\infty & \text{else}     
\end{cases} \\
Y = \text{MaskedAttention}(Q, K, V) = \text{softmax}\left(M \odot \frac{QK^T}{\sqrt{d}}\right) V
\end{gathered}
$$

## Transformer Architecture
### Input Embeddings
* There are two embeddings in a transformer model: token embeddings and positional embeddings.
  * Token embeddings are learned embeddings for each token in the input sequence.
  * Positional embeddings are learned embeddings for the position of each token in the input sequence. Note that self-attention removes the notion of position in the input sequence. 
* The final embedding is the sum of the token and positional embeddings.

### Encoder
* There are three main components in the encoder block: multi-head attention, feed-forward neural network, and normalization layers.

### Decoder
* The decoder block is similar to the encoder block but has two differences
  1. Multi-head self-attention is masked to prevent the decoder from looking at future tokens.
  2. The decoder block has an additional multi-head cross attention layer that takes the encoder output as input. 
* In multi-head cross attention, we use the encoder output as the keys and values and the decoder output as the queries.

### Types of Transformer Architectures
* Encoder-only transformers are transformers with only encoder blocks.
* Likewise decoder-only transformers are transformers with only decoder blocks. These decoder blocks will have masked self-attention, but not cross-attention.
* Here are the main uses of each type of transformer: 

<div class="table-wrapper" markdown="block">

|Type|Common Usage|Examples|
|:-:|:-:|:-:|
|Encoder-Only|Discriminitive analysis of text such as sentiment classificaiton, entity recognition, etc... |BeRT|
|Decoder-Only|Generative tasks such as summarization, question-answering, etc... |GPT-X|
|Encoder-Decoder|Sequence-to-sequence tasks such as translation||

</div>

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


