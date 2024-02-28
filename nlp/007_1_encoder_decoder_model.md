# Week 07.1: Encoder-Decoder Model

**Encoder-decoder** networks, sometimes called sequence-to-sequence networks, are models capable of generating contextually appropriate, arbitrary length, output sequences given an input sequence.

- This architecture is commonly applied to machine translation, where the input sequence and output sequence can have different lengths.
    - Other tasks include summarization, question answering, and dialogue.

**General Encoder-Decoder Process**
1. An **encoder** that accepts an input sequence, $x_{1:n}$, and generates a corresponding sequence of contextualized representations, $h_{1:n}$. LSTMs, convolutional networks, and transformers can all be employed as encoders.
2. A **context vector**, $c$, which is a function of $h_{1:n}$ and conveys the essence of the input to the decoder.
3. A **decoder**, which accepts $c$ as input and generates an arbitrary length sequence of hidden states $h_{1:m}$, from which a corresponding sequence of output
states $y_{1:m}$, can be obtained. Just as with encoders, decoders can be realized
by any kind of sequence architecture.

## Encoder-Decoder Model with RNN
- The encoder will generate a contextualized representation, which is the final hidden state $h_n^e$.
- This representation works as the context $c$ for the decoder network $h_0^d = c$,  and it's **available to each decoder's hidden state** (check picture).
- In the decoder, each hidden state is conditioned on
    1. the previous hidden state, 
    2. the output generated in the previous state, (autoregressive generation step)
    3. the context $c$, which ensures the influence on the context vector (in some architectures).
- In some architectures, it is common to see an encoder with stacked layers and a decoder with stacked layers and BiLSTMs architectures.
    
$$\begin{aligned}
\mathbf{c} & =\mathbf{h}_n^e \\
\mathbf{h}_0^d & =\mathbf{c} \\
\mathbf{h}_t^d & =g\left(\hat{y}_{t-1}, \mathbf{h}_{t-1}^d, \mathbf{c}\right) \\
\mathbf{z}_t & =f\left(\mathbf{h}_t^d\right) \\
y_t & =\operatorname{softmax}\left(\mathbf{z}_t\right)
\end{aligned}$$

- We compute **the most likely output** at each time step by taking the argmax over the softmax output.
$$\hat{y}_t=\text{argmax}_{\mathrm{w} \in \mathrm{V}} P\left(w \mid y_1 \ldots y_{t-1}, x\right)$$
- We compute **the probability of sentence $y$ given input sequence $x$** as
$$p(y \mid x)=p\left(y_1 \mid x\right) p\left(y_2 \mid y_1, x\right) p\left(y_3 \mid y_1, y_2, x\right) \ldots p\left(y_m \mid y_1, \ldots, y_{m-1}, x\right)$$

**Training the Encoder-Decoder Model**
- This model is trained end-to-end, using **teacher forcing**:
    - During training, **teacher forcing** means that we force the system to use the ground truth target token from training as the next input, rather than rely on the (possibly erroneous) decoder output.
        - In other words, we don't consider the autoregressive connection during training.
        - It is because a word badly predicted in the previous step could generate completely different branches.
    - During inference, the decoder uses its own estimated output as the input for the next step. In other words, we consider the autoregressive connection during inference.
- Source and target strings are concatenated with a separator token. Then, starting from the separator token the autoregressive training predicts the next word.


