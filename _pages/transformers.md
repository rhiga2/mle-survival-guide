---
title: Transformers
author: Ryley Higa
date: 2024-07-09
category: deep-learning
ordering: 020
layout: post
---
# Attention
## Scaled Dot-Product Attention
* We are given input queries $Q$, keys $K$, and values $V$.
* We calculate the scaled dot product attention as follows.

$$
\begin{gathered}
Y = \text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right) V
\end{gathered}
$$

## Self-Attention
* Self-attention refers to attention where the queries, keys, and values are all from the same input sequence. As opposed to cross attention where the queries can come from a different input sequence as the keys and values.
* We do this by applying weight matrices to the input $X$.

$$
\begin{gathered}
Q = W^Q X \\
V = W^V X \\
K = W^K X \\
\end{gathered}
$$

## Multi-Head Attention (MHA)
* Sometimes attention depends on different aspects of the input sequence. To capture this intuition, we want to give attention layers different representations of the input sequence $X$.
* We calculate multiple queries, keys, and values by applying different weight matrices $W^Q_i$, $W^K_i$, and $W^V_i$ respectively on the input where $i$ is the index of the head. 
* We then concatenate the outputs of each head and apply a final weight matrix $W^O$ to get the final output.

## Masked Attention
* Sometimes we don't want to give any attention to a future token in the sequence, meaning a query should not retrieve a future key-value pair.
* To do this we zero out the upper triangular portion of the attention matrix before applying the softmax.

$$
\begin{gathered}
M_{ij} = \begin{cases}
   1  & i < j \\
   -\infty & \text{else}     
\end{cases} \\
Y = \text{MaskedAttention}(Q, K, V) = \text{softmax}\left(M \odot \frac{QK^T}{\sqrt{d_k}}\right) V
\end{gathered}
$$

# Transformers
## Input Embeddings
* There are two embeddings in a transformer model: token embeddings and positional embeddings.
  * Token embeddings are learned embeddings for each token in the input sequence.
  * Positional embeddings are learned embeddings for the position of each token in the input sequence. Note that self-attention removes the notion of position in the input sequence. 
* The final embedding is the sum of the token and positional embeddings.

## Encoder
* There are three main components in the encoder block: multi-head attention, feed-forward neural network, and normalization layers.

## Decoder
* The decoder block is similar to the encoder block but has two differences
  1. Multi-head self-attention is masked to prevent the decoder from looking at future tokens.
  2. The decoder block has an additional multi-head cross attention layer that takes the encoder output as input. 
* In multi-head cross attention, we use the encoder output as the keys and values and the decoder output as the queries.

## Output Layer and Loss Function
* Usually we apply a linear layer to the output of the transformer to get the output dimensions in the right format. 
* For example, if we wanted to generate the next token in a sequence, we would apply a linear layer to get a vector with dimensions equal to the number of tokens in the vocabulary. We then feed it into a softmax layer to get the probability of the next token. 

## Types of Transformers
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
