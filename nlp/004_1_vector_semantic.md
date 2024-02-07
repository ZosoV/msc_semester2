# Week 04: Vector Semantic

- A vector semantic is a model of word meaning, which allows us to draw inferences to address meaning-related tasks like question-answering or dialogue.

- In the linguistic study, there are different lexical semantics (desiderata), that have been considered to define our vector semantics.
    - Lemas and Sense:
        - A lemma can be polysemous (have multiple senses)
    - Synonyms:
        - identical (or similar) sense of another word
        - substitutable for another word in any sentence without changing the truth condition of the sentence
    - Word Similarity:
        - Two-word similarity can help to compute how similar the meanings of two sentences are.
    - Word Relatedness:
        - The meaning of two words can be related in ways other than similarity, such as relatedness, or association.
        - One kind of relatedness between words is if they belong to the same semantic field.
    - Semantic Frames and Roles:
        - Distinguish between the roles of entities in a sentence in a particular event.
    - Connotation
        - Words can be grouped by the affective meaning or connotation; which is related to the writer or reader's emotions. (e.g. groups like valence, arousal, dominance)
- Vector semantics is the standard way to represent word meaning in NLP.
- In vector semantics, a word is modeled as a vector—a point in high-dimensional space, also called an **embedding**. In this chapter we focus on **static embeddings**, where each word is mapped to a fixed embedding.
- Vector semantic models fall into two classes: **sparse** and **dense**.

## Sparse Semantic Models

In sparse models each dimension corresponds to a word in the vocabulary V and cells are functions of **co-occurrence counts**. 
- The **term-document matrix** has a row for each word (term) in the vocabulary and a column for each document.
- The **word-context** or **term-term matrix** has a row for each (target) word in the vocabulary and a column for each context term in the vocabulary. 
    - The context can be a whole document or a window (e.g. 4 closer words).
- Raw frequencies are very skewed and not very discriminative (frequently used words like 'the' are not too informative).

- Two sparse weightings are common: **tf-idf** and **PPMI**

### tf-idf (term frequency-inverse document frequency)

The **tf-idf** weighting which weights each cell by its **term frequency** and **inverse document frequency**

- The **term frequency (tf)** corresponds to the frequency of the word $t$ in the document $d$.
        $$\mathrm{tf}_{t, d}= \begin{cases}1+\log _{10} \operatorname{count}(t, d) & \text { if } \operatorname{count}(t, d)>0 \\ 0 & \text { otherwise }\end{cases}$$
- The **inverse document frequency (idf)** corresponds to
    - **df** is the number of documents in which term $t$ occurs, and wrt to the total number of documents $N$, we have.
    $$\frac{\mathrm{df}_t}{N}$$ 
    - If we aim to give a higher weight to words that occur only in a few documents, we can invert this term, as follows
    $$\mathrm{idf}_t = \mathrm{log}_{10}\left(\frac{1}{\frac{\mathrm{df}_t}{N}}\right)$$
    $$\mathrm{idf}_t = \mathrm{log}_{10}\left(\frac{N}{\mathrm{df}_t}\right)$$

- Then, the weight associated to word $t$ in document $d$ is 
$$w_{t,d} = \mathrm{tf}_{t,d} \times \mathrm{idf}_t$$

### **PPMI** (pointwise positive mutual information)
**PPMI** is most common for word-context matrices. It is a measure of how often two events $x$ and $y$ occur, compared with what we would expect (by chance) if they were independent. 

$$\operatorname{PMI}(w, c)=\log _2 \frac{P(w, c)}{P(w) P(c)}$$

Negative values allowed in $PMI$ can be unreliable unless our corpora are enormous. Then, we simplified by
$$\operatorname{PPMI}(w, c)=\mathrm{max}\left(\log _2 \frac{P(w, c)}{P(w) P(c)}, 0\right)$$

In practice,

$$p_{i j}=\frac{f_{i j}}{\sum_{i=1}^W \sum_{j=1}^C f_{i j}}, \quad p_{i *}=\frac{\sum_{j=1}^C f_{i j}}{\sum_{i=1}^W \sum_{j=1}^C f_{i j}}, \quad p_{* j}=\frac{\sum_{i=1}^W f_{i j}}{\sum_{i=1}^W \sum_{j=1}^C f_{i j}}$$

$$\mathrm{PPMI}_{i j}=\max \left(\log _2 \frac{p_{i j}}{p_{i *} p_{* j}}, 0\right)$$

Notice rare words can have low frequencies, which can lead to a lower $P(c)$ and consequently to high PMI values. To avoid that we can use a power of $\alpha$

$$\operatorname{PPMI}_\alpha(w, c)=\max \left(\log _2 \frac{P(w, c)}{P(w) P_\alpha(c)}, 0\right)$$

$$P_\alpha(c)=\frac{\operatorname{count}(c)^\alpha}{\sum_c \operatorname{count}(c)^\alpha}$$

where $P_\alpha(c) > P(c)$.

## Cosine for measuring similarity

The cosine similarity is a normalized dot product between two vectors and measures how similar are two words regardless of their frequency.

It can be used with any two vector representations ("embeddings")

- Notice if we don't normalize we will be given higher similarity to more frequent words.
- In some applications, it's possible to pre-normalize each vector and get the unit vector. Then, the dot product and cosine are the same for unit vectors.
- Because we only work with counts cosine cannot take negative values.

$$\operatorname{cosine}(\mathbf{v}, \mathbf{w})=\frac{\mathbf{v} \cdot \mathbf{w}}{|\mathbf{v}||\mathbf{w}|}=\frac{\sum_{i=1}^N v_i w_i}{\sqrt{\sum_{i=1}^N v_i^2} \sqrt{\sum_{i=1}^N w_i^2}}$$