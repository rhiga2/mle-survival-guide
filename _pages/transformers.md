---
title: Transformers and LLMs
author: Ryley Higa
date: 2024-07-09
category: deep-learning
ordering: 033
layout: post
---
# Transformers
Transformers are a form of deep learning architecture that powers nearly all large language models and is also making state-of-the-art breakthroughs in many vision and reasoning tasks as well. 
The primary architecture component of transformers are **attention mechanisms**. As humans, given a image we don't pay attention to every region in the image equally. For instance, 
we often pay more attention to foreground objects as opposed to background details. Machines need to similar method of assigning importance (called **attention**) to certain components of an input.
Thus attention mechanism should have the following properties:
1. A way of breaking inputs into **value** vectors in which to assign attention. In LLMs, these values can be single token embeddings, whereas in images, these values can be divided regions of an image.   
2. A mechanism to assign attention to each value based on a **query**. In humans, our attention is situational. If you were given an image of a cat and dog and asked a question about the dog,
our attention will focus primarily on the dog. Likewise, if we were to asked a question about the cat, our attention will focus primarily on the cat. 
3. A method to retrieve and aggregate values that prioritizes values assigned the most attention.
Combining all three properties indicates that at the end of the day, attention mechanisms are soft retrieval systems. Soft retrieval refers to fact that the retrieval is not all of nothing.
Retrieving books from a library is an example of hard retrieval as you either check out the whole book or leave without the book. Using this analogy, soft retrieval would be like getting to take
bits and pieces of a bunch of books and splicing it together. Since attention is a form of retrieval, much of the terminology (such as **query, keys, and values**) are lifted from retrieval literature.
In the next section, we will go over a simple attention mechanism scaled dot product attention. 

## Scaled Dot-Product Attention
In scaled dot-product attention we have three inputs: queries $Q$, keys $K$, and values $V$. Suppose that these inputs are vectors of length $d$ (we will discuss later where these inputs come from). 
Similar to database retrieval, each key has an associated value. We assign attention to values based on the keys that are most similar to each query. As you may have guessed by the name, similarity is measured 
as the dot product between queries and keys. Thus queries and keys that point in the same direction are likely to get the highest similarity scores $S$. Note that $d$ has a large impact
on the dot product regardless of actual similarity between the two input vectors. To scale appropriately we divide the input by $\sqrt{d}$. 

$$
\begin{gathered}
S = \frac{QK^T}{\sqrt{d}}
\end{gathered}
$$

Any failed multitasker will know, attention is finite. Paying attention to your phone while driving means less attention is given to the road. On the other hand, similarity scores are 
unbounded values, which makes them unsuitable for directly modelling attention. To make the scores into attentions, we must therefore bound the sum such that an increase of attention to one component results 
in decreased attention to another component. What better way to do this that using the softmax function described in our section on linear models.  

$$
\begin{gathered}
A = \text{softmax}(S) 
\end{gathered}
$$

The final thing to do is to retrieve and aggregate components based on attention. We do this by taking a weighted average of values based on their attention to get the final output $Y$. 

$$
\begin{gathered}
Y = AK
\end{gathered}
$$

## Cross-Attention and Self-Attention
We still have explain a major component of attention mechanisms: where does the QKV triplets come from? The answer is "it depends." In applications like French to English text
translation, our query may come from previous English tokens we have already translated and our key and values may come from the referenced French text we are trying to translate. This
is known as **cross-attention** since queries come from different sources of data. The alternative is **self-attention** where the query, key, and value come from the same source of data. For example,
if we are trying to fill in a missing word in an English sentence our query comes from the sentence with the missing words, but the piece of information we need to reference to fill the gap 
is also the surrounding context. 

Whatever the source of QKV triplets come from, we often don't feed in tokens or data in it's raw format to attention mechanisms. Instead to opt to linearly transform the input into
a QKV triplet. For example, in self-attention given input of embeddings $X$ we get a QKV triplet using three separate linear transformations:

$$
\begin{gathered}
Q = W^Q X \\
V = W^V X \\
K = W^K X \\
\end{gathered}
$$

Combining linear transformations with attention is known as an **attention head**.

## Multi-Head Attention (MHA)
I previously mentioned that attention is finite, which is often the reason why humans are poor multitaskers. That being said there may be different types of attention active at a 
certain time. For example, suppose you are writing the next big Fantasy series. Writing the dialog for the main protagonist requires that the author gives attention
to different aspects of the story that are either currently written or have yet to be written; aspects such as the protagonist's culture, her state of mind, her age, her relationship
to the person she's speaking to, her motivation. To model cases, where attention needs to be given to muliple aspects simultaneously such as in this example, we often employ the usage
of multiple attention heads known as **multi-headed attention**. 

In multi-headed attention, we apply different attention heads to the input, concatenate the results, and then do another linear transformation to combine the concatenated results. 

## Masked or Causal Attention

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
