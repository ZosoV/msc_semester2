1. What is the RNN architecture for each of the following:
    - FNN: one to one
    - RNN for text classification: many to one
    - Machine Translation: many to many, but encoder-decoder
    - Image captioning: one to many
    - Sequence labeling: many to many

2. Why is there a "y" at the calculation of the hidden state $h_t^d$?
$$h_t^d = g(\hat{y}_{t-1}, h_{t-1}^d, c)$$
That y is from the previous step. It's the autoregressive step.