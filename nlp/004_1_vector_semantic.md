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
    - The **tf-idf** weighting which weights each cell by its **term frequency** and **inverse document frequency**
        - use log to calculate tf and also 0 when is zero.
    - **PPMI** (pointwise positive mutual information), which is most common for word-context matrices.
        - TODO: 


## Cosine for measuring similarity

The cosine similarity is a normalized dot product between two vectors and measures how similar are two words regardless of their frequency.

It can be used with any two vector representations ("embeddings")

- Notice if we don't normalize we will be given higher similarity to more frequent words.
- In some applications, it's possible to pre-normalize each vector and get the unit vector. Then, the dot product and cosine are the same for unit vectors.
- Because we only work with counts cosine cannot take negative values.

$$\operatorname{cosine}(\mathbf{v}, \mathbf{w})=\frac{\mathbf{v} \cdot \mathbf{w}}{|\mathbf{v}||\mathbf{w}|}=\frac{\sum_{i=1}^N v_i w_i}{\sqrt{\sum_{i=1}^N v_i^2} \sqrt{\sum_{i=1}^N w_i^2}}$$