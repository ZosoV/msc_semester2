# Week 07.2: Attention

- In normal encoder-decoder models, the final hidden state of the encoder is used as a **static** context.
    - This final hidden state is acting as a **bottleneck**: it must represent **absolutely everything** about the meaning of the source text.
- The attention mechanism allows the decoder to get information from all the hidden states of the encoder, not just the last hidden state.
    - It provides a way to disentangle the compacted information because all the information is not necessarily useful for the current i-th step on the decoder.
    - It would create a **dynamic** context for each step $i$ of the decoder based on all the hidden states of the encoder.
        $$c_i = f(h_1^e \cdots h_n^e)$$
    - ELMO was doing a similar thing as Attention because it also considers all the hidden states to make calculations.
- Note that this dynamic context is generated for each decoding step $i$ as
$$h_i^d = g(\hat{y}_{i-1},h_{i-1}^d, c_i)$$


**Dot-Product Attention and Dynamic Context**

This **dynamic context** is gotten by a weighted average over all the encoder hidden states, where $\alpha_{ij}$ represents a proportional relevance weight of the encoder hidden state $h_j^e$ and the decoder hidden state $h_{i-1}^d$.
$$c_i = \sum_j \alpha_{ij} h_j^e$$

The normalized scores $a_{ij}$ are gotten by
$$\alpha_{ij} = \text{softmax}(\text{score}(h_{j-1}^d,h_j^e))$$
$$\alpha_{ij} = \frac{\text{exp}(\text{score}(h_{i-1}^d,h_j^e))}{\sum_k \text{exp}(\text{score}(h_{i-1}^d,h_k^e))}$$

And the scores are gotten by simple dot-product. For that reason, this attention mechanism is called **dot-product attention**.
- Notice the score captures the similarity between the hidden states from the encoder and decoder and consequently gives a notion of relevance.
    $$\text{score}(\mathbf{h_{i-1}^d},h_j^e) = \mathbf{h_{i-1}^d} \cdot h_j^e$$
- Notice we compare all the encoder hidden states against the i-1 hidden state on step i.

### Extra Takeaways

- It's possible to use more sophisticated scoring functions by parameterizing the score with its own set of weights $W_s$, which are trained to the end-to-end training.
    - It helps to learn which aspects of similarity between the decoder and encoder state are important to the current application.
    - It enables to use of different dimensional hidden states between encoder and decoder.

- In other architectures, attention can be also **learned via a simple FFN** (Check image slides)

- Linear weights are interpretable in some way, but sometimes it's not enough.
    - We can see in an attention matrix, which word is more important.
    - We can use it for explainability but only until a certain point. It's not enough.

