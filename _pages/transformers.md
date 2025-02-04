---
title: Transformers
author: Ryley
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
\begin{gather*}
Y = \text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right) V
\end{gather*}
$$

## Self-Attention
* Self-attention refers to attention where the queries, keys, and values are all from the same input sequence. As opposed to cross attention where the queries can come from a different input sequence as the keys and values.
$$
\begin{gathered}
Q = W^Q X
V = W^V X
K = W^K X
\end{gathered}
$$

## Multi-Head Attention (MHA)
* Sometimes attention depends on different aspects of the input sequence. To capture this intuition, we want to give attention layers different representations of the input sequence $X$.
* We calculate multiple queries, keys, and values by applying different weight matrices $W^Q_i$, $W^K_i$, and $W^V_i$ respectively on the input where $i$ is the index of the head. 
* We then concatenate the outputs of each head and apply a final weight matrix $W^O$ to get the final output.

# Transformers
## Input Embeddings
* There are two embeddings in a transformer model: token embeddings and positional embeddings.
    * Token embeddings are learned embeddings for each token in the input sequence.
    * Positional embeddings are learned embeddings for the position of each token in the input sequence. Note that self-attention removes the notion of position in the input sequence. 
* The final embedding is the sum of the token and positional embeddings.

## Encoder
* There are three main components in the encoder block: multi-head attention, feed-forward neural network, and normalization layers.
    1. Feed input X multi-head self-attention layer
    2. Add input (residual connection) to output and apply normalization layer
    3. Apply feed-forward neural network to output and apply normalization layer

## Decoder
* The decoder block is similar to the encoder block but has two differences
    1. Multi-head self-attention is masked to prevent the decoder from looking at future tokens.
    2. The decoder block has an additional multi-head cross attention layer that takes the encoder output as input.
* To mask multi-head self-attention, we zero out the upper triangular part of the attention matrix that way the decoder can only use previous context to represent tokens. Let $M$ be mask matrix where the lower triangular part is 1 and the rest is $-\infty$.   

$$
\begin{gather*}
Y = \text{MaskedAttention}(Q, K, V) = \text{softmax}\left(M \odot \frac{QK^T}{\sqrt{d_k}}\right) V
\end{gather*}
$$

* In multi-head cross attention, we use the encoder output as the keys and values and the decoder output as the queries.

## Output Layer and Loss Function
* Usually we apply a linear layer to the output of the transformer to get the output dimensions in the right format. 
* For example, if we wanted to generate the next token in a sequence, we would apply a linear layer to get a vector with dimensions equal to the number of tokens in the vocabulary. We then feed it into a softmax layer to get the probability of the next token. 

## Types of Transformers
* Encoder-only transformers are transformers with only encoder blocks. Likewise decoder-only transformers are transformers with only decoder blocks. 
    * Decoder-only transformers do not have the cross-attention layer.
* Here are the main uses of each type of transformer: 

<div class="table-wrapper" markdown="block">

|Type|Common Usage|Examples|
|:-:|:-:|:-:|
|Encoder-Only|Discriminitive analysis of text such as sentiment classificaiton, entity recognition, etc... |BeRT|
|Decoder-Only|Generative tasks such as summarization, question-answering, etc... |GPT-X|
|Encoder-Decoder|Sequence-to-sequence tasks such as translation|Original transformer|

</div>
