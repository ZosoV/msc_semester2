# Week 07.3: Self-Attention

## Self-Attention

Self-attention is a way to compute representations of a word at a given layer by integrating information from words at the previous layer (it is the context).

- Core Intuition: Comparing an item of interest to a collection of other items in a way that reveals their relevance in the current context

In contrast to **dot-product attention**, self-attention includes three different roles based on learned parameters.
1. **query** is the current focus of attention (the current analyzed word/token)
2. **key** is the preceding input identifier.
3. **value** is the preceding valuable information.


- Notice it works as a "hashmap", where you have a query and use it to check different keys in the hashmap, and when matching get the value.

To capture the roles, the transformer introduces weight matrices $W^Q, W^K$, and $W^V$

$$q_i = x_iW^Q; \quad k_i = x_iW^K; \quad v_i = x_iW^V$$

- Notice the dimension are $W^Q \in \mathbb{R}^{d\times d_k}, W^K \in \mathbb{R}^{d\times d_k}$, and $W^V \in \mathbb{R}^{d\times d_V}$

Then, the scores are obtained by

$$\text{score}(x_i,x_j) = q_i \cdot k_j$$

- Notice that this score is related to the dot-product attention score, but now we are using an advanced scoring with learnable parameters.
    - These parameters help us to capture the similarities. $$q_i \cdot k_j = q_ik_j^T = x_iW^Q(W^K)^Tx_i^T = x_i W_s x_i^T$$

- Notice the normalization step provides a probability distribution.

Then, the normalized scores are gotten as before with softmax.
$$\alpha_{ij} = \text{softmax}(\text{score}(h_{j-1}^d,h_j^e))$$

And the output $a_i$

$$a_i = \sum_j \alpha_{ij} v_j^e$$

- Notice here the value $v_j$ works as the hidden state in RNN. It would in some way encode the information from the previous step which is relevant to the current focus of attention.
- Notice the attention will be highest to the current focus, but also will pay more attention to others.

- To avoid numerical issues a dividing factor $\sqrt{d_k}$ is added to the dot product related to the size of the embeddings

**Final Equations:**

$$\begin{aligned}
\mathbf{q}_i=\mathbf{x}_i \mathbf{W}^{\mathbf{Q}} ; \mathbf{k}_i & =\mathbf{x}_i \mathbf{W}^{\mathbf{K}} ; \mathbf{v}_i=\mathbf{x}_i \mathbf{W}^{\mathbf{V}} \\
\text{score}\left(\mathbf{x}_i, \mathbf{x}_j\right) & =\frac{\mathbf{q}_i \cdot \mathbf{k}_j}{\sqrt{d_k}} \\
\alpha_{i j} & =\text{softmax}\left(\text{score}\left(\mathbf{x}_i, \mathbf{x}_j\right)\right) \forall j \leq i \\
\mathbf{a}_i & =\sum_{j \leq i} \alpha_{i j} \mathbf{v}_j
\end{aligned}$$


# Independence and Two Types of Self-Attention

- There are two ways to build transformer systems:

    1. **Backward-looking self-attention** is also called casual (masked), and only access to the current input and inputs before the current input.
    - It helps to create language models and use them for autoregressive generation
    2. **Bidirectional self-attention** has access to all past, future and current inputs.
- The previous explanation used the backward-looking mechanism

- The computation performed for each item is **independent** of all the other computations.
    - Then, it can be easily parallelized both forward inference and training.
    - It's a contrastive difference with RNN, which has to compute all input sequentially.